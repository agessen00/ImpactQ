# ImpactQ — Backend Architecture Plan

**Status:** Planning (Frontend MVP built, backend next)
**Date:** March 26, 2026

---

## Overview

ImpactQ needs to evolve from a single-file browser app to a multi-tenant SaaS platform. This document defines the authentication, authorization, data persistence, and API architecture required.

---

## User Roles (3-Tier RBAC)

| Role | Access Level | Capabilities |
|------|-------------|--------------|
| **Security Master** | Full admin | Create/manage user accounts, assign roles, manage all organizations, configure security settings, audit logs |
| **Strategic User** | Full product | CRUD all objectives & plans, configure org parameters, access Present Mode, view all dashboards, manage team |
| **Product User** | Restricted view | View assigned objectives/plans only, update status on assigned plans, cannot create/delete objectives |

### Permission Matrix

| Action | Security Master | Strategic User | Product User |
|--------|:-:|:-:|:-:|
| Create organization | ✅ | ❌ | ❌ |
| Manage users & roles | ✅ | ❌ | ❌ |
| Create/delete objectives | ✅ | ✅ | ❌ |
| Edit objectives | ✅ | ✅ | ❌ |
| Create/delete tactical plans | ✅ | ✅ | ❌ |
| Edit plan status/progress | ✅ | ✅ | ✅ (assigned only) |
| View all objectives | ✅ | ✅ | 🔒 (assigned only) |
| Access Present Mode | ✅ | ✅ | ✅ (visible objectives) |
| Configure org parameters | ✅ | ✅ | ❌ |
| View audit log | ✅ | ❌ | ❌ |
| Export/import data | ✅ | ✅ | ❌ |

---

## Recommended Tech Stack

### Option A: Supabase (Recommended for MVP)

Supabase provides auth, database, and real-time subscriptions in one platform. Free tier supports up to 50K monthly active users.

- **Auth:** Supabase Auth (email/password, magic link, SSO ready)
- **Database:** PostgreSQL (hosted by Supabase)
- **API:** Auto-generated REST + real-time WebSocket
- **Storage:** Supabase Storage (for file uploads later)
- **Hosting:** GitHub Pages (frontend) + Supabase (backend)
- **Cost:** Free tier → $25/mo Pro when you scale

### Option B: Firebase

- **Auth:** Firebase Auth
- **Database:** Firestore (NoSQL)
- **Hosting:** Firebase Hosting
- **Cost:** Free tier → pay-as-you-go

### Recommendation: **Supabase** — relational data model fits ImpactQ's structured hierarchy, PostgreSQL gives you Row Level Security for the permission system, and the auto-generated API means less custom code.

---

## Database Schema (PostgreSQL)

```sql
-- Organizations (multi-tenant)
CREATE TABLE organizations (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  name TEXT NOT NULL,
  slug TEXT UNIQUE NOT NULL,
  settings JSONB DEFAULT '{}',
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- Users
CREATE TABLE users (
  id UUID PRIMARY KEY REFERENCES auth.users(id),
  email TEXT UNIQUE NOT NULL,
  full_name TEXT NOT NULL,
  avatar_url TEXT,
  created_at TIMESTAMPTZ DEFAULT now()
);

-- Organization membership + roles
CREATE TABLE org_members (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  org_id UUID REFERENCES organizations(id) ON DELETE CASCADE,
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  role TEXT NOT NULL CHECK (role IN ('security_master', 'strategic_user', 'product_user')),
  created_at TIMESTAMPTZ DEFAULT now(),
  UNIQUE(org_id, user_id)
);

-- Strategic Objectives
CREATE TABLE objectives (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  org_id UUID REFERENCES organizations(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  description TEXT,
  sort_order INTEGER DEFAULT 0,
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- Tactical Plans
CREATE TABLE plans (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  objective_id UUID REFERENCES objectives(id) ON DELETE CASCADE,
  org_id UUID REFERENCES organizations(id) ON DELETE CASCADE,
  title TEXT NOT NULL,
  status TEXT NOT NULL DEFAULT 'not_started'
    CHECK (status IN ('not_started', 'in_progress', 'at_risk', 'complete')),
  progress INTEGER DEFAULT 0 CHECK (progress >= 0 AND progress <= 100),
  owner_id UUID REFERENCES users(id),
  owner_name TEXT,
  sort_order INTEGER DEFAULT 0,
  created_by UUID REFERENCES users(id),
  created_at TIMESTAMPTZ DEFAULT now(),
  updated_at TIMESTAMPTZ DEFAULT now()
);

-- Plan assignments (which Product Users can see/edit which plans)
CREATE TABLE plan_assignments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  plan_id UUID REFERENCES plans(id) ON DELETE CASCADE,
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  can_edit BOOLEAN DEFAULT true,
  created_at TIMESTAMPTZ DEFAULT now(),
  UNIQUE(plan_id, user_id)
);

-- Audit log
CREATE TABLE audit_log (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  org_id UUID REFERENCES organizations(id),
  user_id UUID REFERENCES users(id),
  action TEXT NOT NULL,
  entity_type TEXT NOT NULL,
  entity_id UUID,
  details JSONB,
  created_at TIMESTAMPTZ DEFAULT now()
);
```

---

## Row Level Security (RLS) Policies

```sql
-- Users can only see their own org's data
ALTER TABLE objectives ENABLE ROW LEVEL SECURITY;
CREATE POLICY "Users see own org objectives" ON objectives
  FOR SELECT USING (
    org_id IN (SELECT org_id FROM org_members WHERE user_id = auth.uid())
  );

-- Product users only see objectives they're assigned to
CREATE POLICY "Product users see assigned objectives" ON objectives
  FOR SELECT USING (
    EXISTS (
      SELECT 1 FROM org_members
      WHERE user_id = auth.uid() AND org_id = objectives.org_id
      AND (role IN ('security_master', 'strategic_user')
        OR EXISTS (
          SELECT 1 FROM plans p
          JOIN plan_assignments pa ON pa.plan_id = p.id
          WHERE p.objective_id = objectives.id AND pa.user_id = auth.uid()
        ))
    )
  );

-- Only strategic+ can create/delete
CREATE POLICY "Strategic users manage objectives" ON objectives
  FOR ALL USING (
    EXISTS (
      SELECT 1 FROM org_members
      WHERE user_id = auth.uid() AND org_id = objectives.org_id
      AND role IN ('security_master', 'strategic_user')
    )
  );
```

---

## API Endpoints (auto-generated by Supabase, custom RPCs where needed)

| Method | Endpoint | Auth | Description |
|--------|----------|------|-------------|
| GET | `/objectives?org_id=eq.{id}` | Token | List objectives (RLS filtered) |
| POST | `/objectives` | Strategic+ | Create objective |
| PATCH | `/objectives?id=eq.{id}` | Strategic+ | Update objective |
| DELETE | `/objectives?id=eq.{id}` | Strategic+ | Delete objective |
| GET | `/plans?objective_id=eq.{id}` | Token | List plans (RLS filtered) |
| POST | `/plans` | Strategic+ | Create plan |
| PATCH | `/plans?id=eq.{id}` | Assigned+ | Update plan status/progress |
| POST | `/rpc/invite_user` | Security Master | Invite user to org |
| POST | `/rpc/change_role` | Security Master | Change user role |

---

## Migration Path (Current → SaaS)

### Phase 1 (Now): Frontend MVP
- Single HTML file, localStorage
- Data model matches the database schema above
- ✅ DONE

### Phase 2 (Next): Add Supabase
1. Create Supabase project
2. Run the SQL schema above
3. Add Supabase JS client to the HTML file
4. Replace localStorage read/write with Supabase queries
5. Add login/signup screen
6. Deploy frontend to GitHub Pages

### Phase 3: Role-Based Access
1. Implement org_members and role checks
2. Add user management UI (Security Master only)
3. Add plan assignment UI
4. Implement RLS policies

### Phase 4: Multi-Tenant
1. Organization switcher
2. Invite flow (email-based)
3. Org settings page
4. Billing integration (Stripe)

---

## Data Shape Compatibility

The current frontend data model:
```javascript
// Current localStorage format
[{
  id: "abc123",
  title: "Workforce Excellence",
  description: "...",
  plans: [{
    id: "def456",
    title: "Leadership Development",
    status: "complete",
    progress: 95,
    owner: "Ana Torres"
  }]
}]
```

Maps cleanly to the database:
- Each objective becomes a row in `objectives`
- Each plan becomes a row in `plans` with `objective_id` foreign key
- `owner` string becomes `owner_name` + optional `owner_id` reference
- No data restructuring needed when migrating

---

*Document prepared for InsightQ ImpactQ development — March 2026*
