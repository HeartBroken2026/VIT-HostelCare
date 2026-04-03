# [1.1.0](https://github.com/HeartBroken2026/VIT-HostelCare/compare/v1.0.0...v1.1.0) (2026-04-03)


### Features

* add priority-based complaint sorting structure (closes [#7](https://github.com/HeartBroken2026/VIT-HostelCare/issues/7)) ([a39cf8c](https://github.com/HeartBroken2026/VIT-HostelCare/commit/a39cf8c73af91022b65721603cf23064994c9ee2))
* add semantic-release for automated versioning and changelog ([032d3a5](https://github.com/HeartBroken2026/VIT-HostelCare/commit/032d3a54c03889db916cb16cb14fbda8443ff7fc))

# Changelog
## VIT HostelCare — Hostel Complaint Management System

All notable changes to this project are documented in this file.

This project adheres to [Semantic Versioning](https://semver.org/).

---

## [v1.0.0] — March 2026

### Initial Release

First production-ready release of VIT HostelCare. This release introduces the complete hostel complaint management system with role-based access for students, admins, and workers.

### Added

#### Student Module (`feature/student-dashboard`)
- Student registration and login via Supabase Auth
- Complaint submission form with category selection
- Real-time complaint status tracking (Pending → Ongoing → Resolved)
- Personal complaint history view

#### Admin / Warden Module (`feature/admin-dashboard`)
- Admin dashboard showing all complaints across the hostel
- Ability to assign workers to specific complaints
- Complaint status management and resolution monitoring
- Overview of pending, ongoing, and resolved complaints

#### Worker Module (`feature/worker-dashboard`)
- Worker login using email credentials
- View of complaints assigned by admin
- Ability to update complaint progress
- Mark complaints as resolved

#### Database & Authentication (`feature/supabase-schema`)
- Supabase Auth integration for all three roles
- Database schema for complaints, users, and worker tables
- Role-based access control at the database level
- Structured complaint lifecycle management

#### Infrastructure
- GitHub Actions CI pipeline for automated builds on every push
- `.gitignore` configured to exclude `node_modules`, `.env`, `.next`
- Repository structured with `src/`, `public/`, `supabase/` directories

### Technical Stack
- **Frontend:** React, Next.js 16 (App Router), TypeScript, Tailwind CSS
- **Backend:** Next.js API Routes, Server Actions
- **Database & Auth:** Supabase
- **CI/CD:** GitHub Actions
- **Version Control:** Git + GitHub

---

## [Unreleased] — Future Improvements

The following features are planned for upcoming releases:

- `v1.1.0` — Image upload support for complaint evidence
- `v1.1.0` — Email and push notifications for status updates
- `v1.2.0` — Priority-based complaint sorting and escalation
- `v1.2.0` — Analytics dashboard for admin
- `v1.3.0` — Worker performance tracking and ratings
- `v2.0.0` — Mobile application (React Native)
