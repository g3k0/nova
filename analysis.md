# Hybrid Architecture Analysis: Next.js + Strapi Self-Hosted (Community Edition)

## Project Goal
Build an author-focused personal website with:
- highly curated visual quality;
- autonomous publishing of stories and literary works;
- a secure admin area for content management;
- potential extension to a user post section (blog-style).

The selected architecture clearly separates:
- **frontend**: Next.js (rendering, UX/UI, performance, SEO);
- **content layer**: Strapi Community Edition, self-hosted (editorial workflow, roles, content APIs).

---

## Final Decision
The project adopts **Option A hybrid** with:
- **Next.js custom frontend**
- **Strapi self-hosted (Community Edition)**
- **No Sanity**

This matches the explicit constraint: **zero software licensing cost**, while accepting higher technical workload.

---

## Why This Setup Fits

### Main Advantages
1. **Zero license cost**
   - Strapi Community Edition is free and open source;
   - no per-seat SaaS fees for CMS usage.

2. **No-compromise frontend design**
   - Next.js remains fully custom for premium literary UX/UI;
   - editorial identity is independent of CMS theming constraints.

3. **Strong control and low vendor lock-in**
   - full ownership of infrastructure, data, and deployment strategy;
   - easier long-term autonomy for architecture changes.

4. **Extensible content model**
   - easy to add content types (stories, static pages, optional user posts);
   - APIs can serve web, mobile, and future channels.

5. **Scalable by architecture, not by subscription tier**
   - growth is handled through infra decisions (resource scaling, caching, CDN), not seat pricing.

### Trade-offs / Risks
1. **Higher operational burden**
   - patching, upgrades, backups, observability, and incident response are fully your responsibility.

2. **Security accountability**
   - hardening Strapi/API, secret management, role permissions, and network boundaries require careful setup.

3. **Time cost replaces subscription cost**
   - no license fee, but meaningful engineering effort for maintenance.

4. **Infrastructure cost can still exist**
   - software is free, but domain/hosting/storage/power are external costs if not already available.

---

## Approved MVP Technical Stack
- **Frontend**: Next.js (App Router) + TypeScript + Tailwind or CSS Modules.
- **CMS**: Strapi Community Edition (self-hosted).
- **Database**: PostgreSQL (preferred) or SQLite for very early local bootstrap.
- **Media**: local filesystem at MVP (optional migration to S3-compatible storage later).
- **Admin auth**: managed by Strapi roles/permissions (no custom admin panel in frontend for MVP).
- **Runtime/Deployment**:
  - Docker Compose for local/staging/prod parity;
  - Nginx reverse proxy + Let's Encrypt TLS;
  - optional self-hosted CI/CD pipeline.

---

## MVP Roadmap (6-8 Weeks)

## Phase 0 - Discovery and Foundations (2-3 days)
- define site IA: Home, Archive, Story Detail, About, Contact;
- define visual direction (typography, spacing system, color palette, layout rules);
- define MVP KPIs: publish speed, minimum Core Web Vitals, baseline SEO.

**Deliverables**:
- page map;
- concise visual direction;
- prioritized MVP backlog.

## Phase 1 - Platform Bootstrap (1 week)
- bootstrap Next.js + TypeScript frontend;
- initialize Strapi CE self-hosted project;
- configure PostgreSQL and environment variables;
- model core content types:
  - `AuthorProfile`
  - `Story` (title, slug, cover, excerpt, body, tags, publishDate, status)
  - `Page` (static sections)
  - optional `UserPost` (schema only, public publishing disabled in MVP);
- establish Docker Compose stack and baseline run scripts.

**Deliverables**:
- working local full stack (Next.js + Strapi + DB);
- validated content schema;
- initial environment setup documentation.

## Phase 2 - Public Frontend (2 weeks)
- implement custom UI:
  - editorial Home
  - story Archive (basic filters)
  - story detail page
  - static pages;
- integrate Strapi APIs in Next.js;
- implement SEO-friendly slug routing;
- add loading/error states and media fallbacks.

**Deliverables**:
- complete frontend with real CMS data;
- stable end-to-end user navigation.

## Phase 3 - Editorial Workflow and Security (1 week)
- configure Strapi roles (admin/editor);
- implement draft -> review -> publish flow;
- enable preview for unpublished content;
- implement revalidation strategy in Next.js after publish/update;
- harden stack: CORS, rate limiting, secret rotation, admin access restrictions.

**Deliverables**:
- autonomous editorial flow via Strapi admin;
- secure baseline for production exposure.

## Phase 4 - Quality, SEO, and Operations (1 week)
- dynamic metadata (title, description, Open Graph);
- sitemap and robots;
- performance baseline (image optimization, cache strategy, lazy loading);
- add minimal observability (logs, uptime checks, backup verification).

**Deliverables**:
- technical SEO baseline;
- operational checklist with backup/restore validation.

## Phase 5 - MVP Launch (3-4 days)
- cross-browser/mobile tests;
- editorial regression checks;
- production rollout with rollback plan;
- post-launch stabilization window.

**Deliverables**:
- MVP live;
- runbook for routine operations and incident handling.

---

## "User Blog-Style Posts" Scope
To protect MVP timeline:
- **MVP**: keep only schema + placeholder page (or restricted/private area);
- **Post-MVP**:
  - user registration/auth;
  - moderation workflow;
  - anti-spam/abuse mechanisms;
  - policy and GDPR compliance.

This prevents community complexity from delaying the editorial core launch.

---

## Zero-Cost Constraint Clarification
Under this decision, **software licensing is zero-cost**.  
Potential non-software costs may still apply:
- domain registration;
- hosting/VPS (if not self-provided);
- backup storage;
- external email/monitoring services (if adopted).

If required, these can be minimized with self-hosted alternatives, trading additional maintenance time.

---

## MVP Success Criteria
- publish a new story in < 10 minutes through Strapi admin;
- mobile Lighthouse >= 85 on key pages;
- no blocking Core Web Vitals issues;
- correct SEO indexing for Home, Archive, and Story Detail pages;
- successful backup and restore test before launch.

---

## Key Risks and Mitigations
- **Risk**: delays from highly custom UI  
  **Mitigation**: define a minimal reusable design system in Phase 1.

- **Risk**: operational overload from self-hosting  
  **Mitigation**: automate backup, health checks, and deployment scripts early.

- **Risk**: security misconfiguration on CMS/admin  
  **Mitigation**: enforce least-privilege roles, protect admin route, and schedule update patch windows.

- **Risk**: tight coupling between frontend and CMS data shape  
  **Mitigation**: create a frontend content service layer to isolate API mapping.

---

## Conclusion
For this project and constraint set, **Next.js + Strapi self-hosted (Community Edition)** is the selected architecture.  
It preserves top-tier frontend quality, keeps software license cost at zero, and remains scalable, with the explicit trade-off of higher engineering and operational responsibility.
