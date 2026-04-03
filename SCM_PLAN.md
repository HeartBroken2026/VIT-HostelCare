# Software Configuration Management Plan
## VIT HostelCare — Hostel Complaint Management System

**Version:** 1.1.0  
**Author:** Prince Kumar  
**Date:** April 2026  
**Tech Stack:** Next.js 16, TypeScript, Tailwind CSS, Supabase

---

## 1. Introduction

This document describes the Software Configuration Management (SCM) plan for the VIT HostelCare project — a full-stack web application for managing hostel complaints at VIT. It outlines the tools selected, the rationale behind those choices, branching strategy, commit conventions, versioning policy, and the CI/CD pipeline implemented.

SCM is the discipline of tracking and controlling changes in software. It ensures that every version of the software is reproducible, every change is traceable, and teams can collaborate without overwriting each other's work.

---

## 2. SCM Tools Used

This project uses the following tools across all SCM categories:

| Category | Tool Used | Purpose |
|---|---|---|
| Version Control | Git | Branching, merging, conflict resolution, tagging |
| Remote Hosting | GitHub | Remote repository, Pull Requests, network graph |
| Issue Tracking | GitHub Issues | Task management, bug tracking, feature requests |
| CI/CD | GitHub Actions | Automated build and test pipeline on every push |
| Automated Testing | Vitest | Unit tests running in the CI pipeline |
| Release Automation | Semantic Release | Auto versioning, changelog generation, GitHub Releases |

---

## 3. SCM Tools Overview and Comparison

### 3.1 Version Control Systems

| Tool | Type | Key Characteristics | Used? |
|---|---|---|---|
| **Git** | Distributed | Every developer has full history; supports branching, merging, tagging | Yes |
| SVN (Subversion) | Centralized | Single central server; simpler but no offline commits | No |
| Mercurial | Distributed | Similar to Git; used by Facebook historically but now largely replaced | No |
| Perforce (Helix Core) | Centralized | Industry standard for game development; handles large binary files well | No |

**Justification for Git:** Git was chosen because it is the industry standard for distributed version control. It supports parallel development through branching, allows offline commits, and integrates seamlessly with GitHub. Its widespread adoption means extensive documentation and tooling support.

---

### 3.2 Remote Hosting Platforms

| Tool | Key Characteristics | Used? |
|---|---|---|
| **GitHub** | Most widely used; built-in PRs, Issues, Actions, Releases | Yes |
| GitLab | Strong built-in CI/CD; popular in enterprise environments | No |
| Bitbucket | Tight Atlassian/Jira integration; popular in enterprise teams | No |
| Gitea | Self-hosted lightweight option | No |

**Justification for GitHub:** GitHub was chosen for its seamless integration with Git, built-in Pull Request workflow, GitHub Issues for lightweight task tracking, GitHub Actions for CI/CD, and GitHub Releases for versioning — all available for free on public repositories.

---

### 3.3 Issue Tracking

| Tool | Key Characteristics | Used? |
|---|---|---|
| **GitHub Issues** | Built into GitHub; lightweight; links to commits and PRs | Yes |
| Jira | Enterprise-grade; supports sprints, epics, roadmaps | No |
| Trello | Kanban-style; visual and simple | No |
| Linear | Modern, fast issue tracker popular with startups | No |

**Justification for GitHub Issues:** Since the project is hosted on GitHub, GitHub Issues was the natural choice. It allows issues to be referenced directly in commit messages (e.g. `closes #7`) and closed automatically on merge, creating a clear audit trail between tasks and code changes.

### Issues Tracked

| Issue | Title | Status |
|---|---|---|
| #4 | Add image upload support for complaint evidence | Open |
| #5 | Implement email notifications for status updates | Open |
| #6 | Add analytics dashboard for admin | Open |
| #7 | Priority-based complaint sorting | Closed via commit |

Issue #7 was closed automatically when the commit `feat: add priority-based complaint sorting structure (closes #7)` was merged into `main` — demonstrating Git + GitHub Issues integration.

---

### 3.4 CI/CD Tools

| Tool | Key Characteristics | Used? |
|---|---|---|
| **GitHub Actions** | Built into GitHub; YAML-based; free for public repos | Yes |
| Jenkins | Open-source; highly configurable; requires separate server setup | No |
| CircleCI | Cloud-based; fast parallel builds | No |
| Travis CI | Simple configuration; historically popular in open source | No |

**Justification for GitHub Actions:** GitHub Actions was chosen because it requires zero additional infrastructure — it runs directly within the GitHub repository. For a project of this scale, setting up a Jenkins server would be unnecessary overhead. GitHub Actions automatically triggers on every push and pull request, providing immediate feedback on build health.

---

### 3.5 Automated Testing

| Tool | Key Characteristics | Used? |
|---|---|---|
| **Vitest** | Fast, modern test runner built for Vite/Next.js projects | Yes |
| Jest | Most popular JS test runner; slightly slower than Vitest | No |
| Cypress | End-to-end browser testing | No |
| Playwright | Cross-browser end-to-end testing by Microsoft | No |

**Justification for Vitest:** Vitest was already configured in the project (`vitest.config.ts`) making it the natural choice. It is fast, modern, and integrates directly into the CI pipeline via GitHub Actions.

### Tests Written

```
src/__tests__/hostelcare.test.ts

✓ should validate complaint status transitions
✓ should validate user roles
✓ should validate complaint object has required fields

3 tests passing
```

---

### 3.6 Release Automation

| Tool | Key Characteristics | Used? |
|---|---|---|
| **Semantic Release** | Reads commit messages; auto bumps version; generates changelog | Yes |
| Standard Version | Similar to semantic-release but manual trigger | No |
| Release Please | Google's release automation tool for GitHub | No |
| Manual tagging | `git tag -a v1.0.0` — fully manual | Used initially |

**Justification for Semantic Release:** Semantic Release automates the entire release process by reading Conventional Commit messages and determining the next version number automatically. A `feat:` commit triggers a minor version bump, a `fix:` triggers a patch bump, and a breaking change triggers a major bump. This eliminates human error in versioning and ensures the changelog is always accurate and up to date.

---

## 4. Repository Structure

```
VIT-HostelCare/
├── .github/
│   └── workflows/
│       └── ci.yml              # GitHub Actions CI + Release pipeline
├── public/                     # Static assets
├── src/
│   ├── __tests__/
│   │   └── hostelcare.test.ts  # Vitest unit tests
│   ├── STUDENT_MODULE.md
│   ├── ADMIN_MODULE.md
│   ├── WORKER_MODULE.md
│   └── PRIORITY_SORTING.md
├── supabase/
│   └── SCHEMA_NOTES.md
├── .releaserc.json             # Semantic Release configuration
├── .gitignore
├── CHANGELOG.md                # Auto-generated by Semantic Release
├── README.md                   # CI badge + project overview
├── SCM_PLAN.md                 # This document
├── vitest.simple.config.ts     # Vitest config for CI
├── next.config.mjs
├── package.json
└── tsconfig.json
```

---

## 5. Branching Strategy

This project follows a **Feature Branch Workflow** — all new features and fixes are developed in dedicated branches and merged into `main` via Pull Requests.

### 5.1 Branch Naming Convention

| Branch Type | Pattern | Example |
|---|---|---|
| Feature | `feature/<module-name>` | `feature/student-dashboard` |
| Bug fix | `bugfix/<issue-description>` | `bugfix/fix-room-allotment` |
| Hotfix | `hotfix/<description>` | `hotfix/auth-null-pointer` |
| Release | `release/<version>` | `release/v1.0.0` |

### 5.2 Branches Created

| Branch | Purpose | Status |
|---|---|---|
| `main` | Production-ready code | Active |
| `feature/student-dashboard` | Student complaint submission and tracking | Merged |
| `feature/admin-dashboard` | Admin complaint management and worker assignment | Merged |
| `feature/worker-dashboard` | Worker view for assigned complaints | Merged |
| `feature/supabase-schema` | Supabase database schema documentation | Merged |
| `feature/priority-sorting` | Priority-based complaint sorting (closes #7) | Merged |
| `feature/vitest-tests` | Vitest unit tests setup | Merged |

### 5.3 Branch Protection Rules

- No direct commits to `main`
- All changes go through Pull Requests
- CI pipeline must pass before merge is allowed

---

## 6. Commit Message Convention

This project follows the **Conventional Commits** specification. Semantic Release depends on this to determine version bumps automatically.

### Format
```
<type>: <short description>
```

### Types and Version Impact

| Type | Purpose | Version bump |
|---|---|---|
| `feat` | New feature | Minor (1.0.0 → 1.1.0) |
| `fix` | Bug fix | Patch (1.0.0 → 1.0.1) |
| `docs` | Documentation | No bump |
| `ci` | CI/CD configuration | No bump |
| `test` | Adding tests | No bump |
| `chore` | Maintenance | No bump |
| `BREAKING CHANGE` | Breaking API change | Major (1.0.0 → 2.0.0) |

### Key Commits

| Commit | Message |
|---|---|
| `48f20e2` | first commit |
| `25b320a` | feat: add student complaint submission and status tracking |
| `afddca9` | feat: add admin dashboard for complaint management and worker assignment |
| `e135a46` | feat: add worker dashboard for assigned complaints and resolution updates |
| `082cbeb` | fix: resolve merge conflict between main and feature/student-dashboard |
| `f7096c9` | ci: add GitHub Actions workflow for lint, typecheck and build |
| various | feat: add priority-based complaint sorting structure (closes #7) |
| various | test: add unit tests for complaint status, roles and validation |
| various | feat: add semantic-release for automated versioning and changelog |

---

## 7. Merge Conflict Resolution

During development, a deliberate merge conflict was introduced and resolved to demonstrate the conflict resolution process.

### Scenario
Both `main` and `feature/student-dashboard` modified the same line in `README.md` — the project description — resulting in a conflict when merging.

### Conflict Markers
```
<<<<<<< HEAD
This project uses Next.js, Supabase and TypeScript to streamline hostel complaint management at VIT.
=======
Built with Next.js and Supabase, this system enables students to submit and track hostel complaints in real time.
>>>>>>> feature/student-dashboard
```

### Resolution
Both changes were combined into a single coherent description:
```
This project uses Next.js, Supabase and TypeScript to streamline hostel complaint
management at VIT, enabling students to submit and track complaints in real time.
```

The resolved file was staged, committed with message `fix: resolve merge conflict between main and feature/student-dashboard`, and pushed to `main`.

---

## 8. Versioning Policy

This project follows **Semantic Versioning (SemVer)**: `MAJOR.MINOR.PATCH`

| Component | Meaning | Example trigger |
|---|---|---|
| MAJOR | Breaking changes | Complete system redesign |
| MINOR | New features, backward compatible | Adding notifications module |
| PATCH | Bug fixes | Fixing a form validation error |

Versions are managed automatically by **Semantic Release** — no manual tagging required after the initial setup. Every push to `main` with a `feat:` or `fix:` commit triggers a new release automatically.

### Releases

| Tag | Description | How created |
|---|---|---|
| `v1.0.0` | Initial release — all dashboards with Supabase | Manual `git tag` |
| subsequent | Auto-generated by Semantic Release | Automatic on push to main |

---

## 9. CI/CD Pipeline

A GitHub Actions workflow is configured at `.github/workflows/ci.yml` with two jobs — **build** and **release**.

### Pipeline Flow

```
git push to main / pull request
            ↓
        [ build job ]
            ↓
  Checkout code (actions/checkout@v4)
            ↓
  Setup Node.js 22
            ↓
  Install dependencies (npm install)
            ↓
  Run Vitest unit tests (3 tests)
            ↓
  Build project (npm run build)
            ↓
     Pass ✅ / Fail ❌
            ↓ (only if push to main and build passes)
       [ release job ]
            ↓
  Semantic Release reads commit messages
            ↓
  Bumps version in package.json
            ↓
  Updates CHANGELOG.md
            ↓
  Creates GitHub Release with release notes
```

### Triggers
- Every push to `main` — runs both build and release jobs
- Every push to `feature/*` — runs build job only
- Every Pull Request to `main` — runs build job only

---

## 10. .gitignore Configuration

The following are excluded from version control:

```
node_modules/       # Dependencies (installed via npm install)
.env                # Environment variables (Supabase credentials)
.env.local          # Local environment overrides
.next/              # Next.js build output
*.log               # Log files
```

Sensitive credentials (Supabase URL, API keys) are never committed to the repository. In the CI/CD pipeline, placeholder values are used for the build step.

---

## 11. Summary

This project demonstrates a complete, production-grade SCM workflow using six industry-standard tools working together:

- **Git** — distributed version control with feature branching and conflict resolution
- **GitHub** — remote hosting with Pull Requests, network graph, and Releases
- **GitHub Issues** — lightweight task tracking with automatic closure via commit messages
- **GitHub Actions** — automated CI/CD pipeline running on every push
- **Vitest** — automated unit testing integrated into the CI pipeline
- **Semantic Release** — fully automated versioning, changelog generation, and GitHub Releases

The result is full traceability from task → branch → commit → pull request → test → build → release, which is the core goal of any SCM process.
