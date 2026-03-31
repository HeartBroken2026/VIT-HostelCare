# Software Configuration Management Plan
## VIT HostelCare — Hostel Complaint Management System

**Version:** 1.0.0  
**Author:** Prince Kumar  
**Date:** March 2026  
**Tech Stack:** Next.js 16, TypeScript, Tailwind CSS, Supabase

---

## 1. Introduction

This document describes the Software Configuration Management (SCM) plan for the VIT HostelCare project — a full-stack web application for managing hostel complaints at VIT. It outlines the tools selected, the rationale behind those choices, branching strategy, commit conventions, versioning policy, and the CI/CD pipeline implemented.

SCM is the discipline of tracking and controlling changes in software. It ensures that every version of the software is reproducible, every change is traceable, and teams can collaborate without overwriting each other's work.

---

## 2. SCM Tools Overview and Comparison

The following tools were evaluated for this project across different SCM categories.

### 2.1 Version Control Systems

| Tool | Type | Key Characteristics | Used? |
|---|---|---|---|
| **Git** | Distributed | Every developer has full history; supports branching, merging, tagging | Yes |
| SVN (Subversion) | Centralized | Single central server; simpler but no offline commits | No |
| Mercurial | Distributed | Similar to Git; used by Facebook historically but now largely replaced by Git | No |
| Perforce (Helix Core) | Centralized | Industry standard for game development; handles large binary files well | No |

**Justification for Git:** Git was chosen because it is the industry standard for distributed version control. It supports parallel development through branching, allows offline commits, and integrates seamlessly with GitHub. Its widespread adoption means extensive documentation and tooling support.

---

### 2.2 Remote Hosting Platforms

| Tool | Key Characteristics | Used? |
|---|---|---|
| **GitHub** | Most widely used; built-in PRs, Issues, Actions, Releases | Yes |
| GitLab | Strong built-in CI/CD; popular in enterprise environments | No |
| Bitbucket | Tight Atlassian/Jira integration; popular in enterprise teams | No |
| Gitea | Self-hosted lightweight option | No |

**Justification for GitHub:** GitHub was chosen for its seamless integration with Git, built-in Pull Request workflow, GitHub Issues for lightweight task tracking, GitHub Actions for CI/CD, and GitHub Releases for versioning — all available for free on public repositories.

---

### 2.3 Issue Tracking

| Tool | Key Characteristics | Used? |
|---|---|---|
| **GitHub Issues** | Built into GitHub; lightweight; links to commits and PRs | Yes |
| Jira | Enterprise-grade; supports sprints, epics, roadmaps | No |
| Trello | Kanban-style; visual and simple | No |
| Linear | Modern, fast issue tracker popular with startups | No |

**Justification for GitHub Issues:** Since the project is hosted on GitHub, GitHub Issues was the natural choice. It allows issues to be referenced directly in commit messages (e.g. `fixes #1`) and closed automatically on merge, creating a clear audit trail between tasks and code changes.

---

### 2.4 CI/CD Tools

| Tool | Key Characteristics | Used? |
|---|---|---|
| **GitHub Actions** | Built into GitHub; YAML-based; free for public repos | Yes |
| Jenkins | Open-source; highly configurable; requires separate server setup | No |
| CircleCI | Cloud-based; fast parallel builds | No |
| Travis CI | Simple configuration; historically popular in open source | No |

**Justification for GitHub Actions:** GitHub Actions was chosen because it requires zero additional infrastructure — it runs directly within the GitHub repository. For a project of this scale, setting up a Jenkins server would be unnecessary overhead. GitHub Actions automatically triggers on every push and pull request, providing immediate feedback on build health.

---

### 2.5 Artifact Management

| Tool | Key Characteristics | Used? |
|---|---|---|
| JFrog Artifactory | Enterprise artifact repository for binaries and packages | No |
| Nexus Repository | Open-source artifact manager widely used in Java ecosystems | No |
| GitHub Releases | Lightweight release tagging built into GitHub | Yes |

**Justification:** For a web application of this scale, full artifact management tools like JFrog or Nexus are unnecessary. GitHub Releases provides sufficient versioning and release documentation capability.

---

## 3. Repository Structure

```
VIT-HostelCare/
├── .github/
│   └── workflows/
│       └── ci.yml          # GitHub Actions CI pipeline
├── public/                 # Static assets
├── src/                    # Application source code
│   ├── STUDENT_MODULE.md   # Student module documentation
│   ├── ADMIN_MODULE.md     # Admin module documentation
│   └── WORKER_MODULE.md    # Worker module documentation
├── supabase/               # Supabase schema and migrations
│   └── SCHEMA_NOTES.md     # Database schema documentation
├── .gitignore
├── CHANGELOG.md            # Version history
├── README.md               # Project overview
├── SCM_PLAN.md             # This document
├── next.config.mjs
├── package.json
└── tsconfig.json
```

---

## 4. Branching Strategy

This project follows a **Feature Branch Workflow** — all new features and fixes are developed in dedicated branches and merged into `main` via Pull Requests.

### 4.1 Branch Naming Convention

| Branch Type | Pattern | Example |
|---|---|---|
| Feature | `feature/<module-name>` | `feature/student-dashboard` |
| Bug fix | `bugfix/<issue-description>` | `bugfix/fix-room-allotment` |
| Hotfix | `hotfix/<description>` | `hotfix/auth-null-pointer` |
| Release | `release/<version>` | `release/v1.0.0` |

### 4.2 Branches Created

| Branch | Purpose | Status |
|---|---|---|
| `main` | Production-ready code | Active |
| `feature/student-dashboard` | Student complaint submission and tracking | Merged |
| `feature/admin-dashboard` | Admin complaint management and worker assignment | Merged |
| `feature/worker-dashboard` | Worker view for assigned complaints | Merged |
| `feature/supabase-schema` | Supabase database schema documentation | Merged |

### 4.3 Branch Protection Rules

- No direct commits to `main`
- All changes go through Pull Requests
- At least one review before merge
- CI pipeline must pass before merge is allowed

---

## 5. Commit Message Convention

This project follows the **Conventional Commits** specification for all commit messages.

### Format
```
<type>: <short description>
```

### Types

| Type | Purpose | Example |
|---|---|---|
| `feat` | New feature | `feat: add student complaint submission form` |
| `fix` | Bug fix | `fix: resolve merge conflict in README` |
| `docs` | Documentation changes | `docs: update project description in README` |
| `ci` | CI/CD configuration | `ci: add GitHub Actions workflow` |
| `refactor` | Code refactoring | `refactor: simplify complaint status logic` |
| `chore` | Maintenance tasks | `chore: update dependencies` |

### Commit History (Key Commits)

| Commit | Message | Branch |
|---|---|---|
| `48f20e2` | first commit | main |
| `25b320a` | feat: add student complaint submission and status tracking | feature/student-dashboard |
| `afddca9` | feat: add admin dashboard for complaint management and worker assignment | feature/admin-dashboard |
| `e135a46` | feat: add worker dashboard for assigned complaints and resolution updates | feature/worker-dashboard |
| `082cbeb` | fix: resolve merge conflict between main and feature/student-dashboard | main |
| `35cd159` | Merge pull requests from all feature branches | main |
| `f7096c9` | ci: add GitHub Actions workflow for lint, typecheck and build | main |

---

## 6. Merge Conflict Resolution

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
This project uses Next.js, Supabase and TypeScript to streamline hostel complaint management at VIT, enabling students to submit and track complaints in real time.
```

The resolved file was staged, committed with message `fix: resolve merge conflict between main and feature/student-dashboard`, and pushed to `main`.

---

## 7. Versioning Policy

This project follows **Semantic Versioning (SemVer)**: `MAJOR.MINOR.PATCH`

| Component | Meaning | Example trigger |
|---|---|---|
| MAJOR | Breaking changes | Complete system redesign |
| MINOR | New features, backward compatible | Adding notifications module |
| PATCH | Bug fixes | Fixing a form validation error |

### Releases

| Tag | Description | Date |
|---|---|---|
| `v1.0.0` | Initial release — student, admin, worker dashboards with Supabase integration | March 2026 |

Tags are created using annotated Git tags and published as GitHub Releases with full release notes.

---

## 8. CI/CD Pipeline

A GitHub Actions workflow was configured at `.github/workflows/ci.yml` to automatically run on every push to `main` or any `feature/*` branch, and on every Pull Request targeting `main`.

### Pipeline Steps

```
git push / pull request
        ↓
Checkout code (actions/checkout@v4)
        ↓
Setup Node.js 22 (actions/setup-node@v4)
        ↓
Install dependencies (npm install)
        ↓
Build project (npm run build)
        ↓
Pass ✅ / Fail ❌
```

### Benefits
- Catches build errors before they reach `main`
- Every PR is validated automatically
- Build status badge visible on repository homepage
- Zero additional infrastructure required

---

## 9. .gitignore Configuration

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

## 10. Summary

This project demonstrates a complete SCM workflow using industry-standard tools:

- **Git** for distributed version control with feature branching
- **GitHub** for remote hosting, Pull Requests, Issues, and Releases
- **GitHub Actions** for automated CI/CD on every push
- **Conventional Commits** for a clean, readable commit history
- **Semantic Versioning** for structured release management
- **GitHub Issues** for lightweight task and bug tracking

The combination of these tools provides full traceability from task → branch → commit → pull request → release, which is the core goal of any SCM process.
