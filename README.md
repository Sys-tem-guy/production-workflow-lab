# Production Git Workflow Lab: Trunk-Based Branching & Release Pipeline

A production-grade demonstration of version control engineering, atomic commits, isolated feature branching, and zero-conflict integration practices.

---

## 📌 Executive Summary
In high-velocity DevOps environments, unstable code integrations cause costly downtime and broken builds. This lab establishes a strict production Git branching strategy. By enforcing feature branch isolation, structured conventional commits, fast-forward zero-conflict integration, and branch lifecycle management, this project demonstrates how to safeguard the `main` branch as a continuously deployable release stream.

---

## 🏗️ Architecture & Branching Strategy

```text
  main (production)
   │
   ├───────────────┐ (git switch -c feature/add-service-healthcheck)
   │               │
   │               ▼
   │          [Feature Branch]
   │          * Add healthcheck.sh
   │          * Atomic conventional commit
   │               │
   ├───────────────┘ (git merge feature/add-service-healthcheck)
   │
   ▼
  main (release updated & branch pruned)
```
- *Trunk Branch (main):* Protected, always-green production release channel.

- *Feature Branches (feature/*):* Ephemeral, single-responsibility branches isolated from production.

- *Commit Standards:* Conventional Commits format (feat:, fix:, chore:) to automate semantic versioning and changelog parsing.

## 🛠️ Implementation Highlights
1. *Workspace Initialization & Identity Isolation:* Configured deterministic identity tracking and locked an immutable baseline commit on the default release branch.

2. *Isolated Feature Branching:* Branched off main to decouple development risk from running workloads.

3. *Artifact Construction & Atomic Commits:* Developed an executable container/service health monitoring script (healthcheck.sh), setting exact POSIX permissions (755) and packaging the change in a single 
scoped commit.

4. *Fast-Forward Production Merge:* Re-integrated the feature branch cleanly into main without creating superfluous merge commits.

5. *Branch Hygiene & Pruning:* Enforced lifecycle cleanup by deleting local tracking branches post-merge to prevent branch drift.

## 📂 Repository Structure
```plaintext
production-workflow-lab/
├── README.md          # Project overview, architectural flow, and verification guide
└── healthcheck.sh     # Executable endpoint health inspection utility
```

## 🚀 Step-by-Step Reproduction Guide
1. *Clone & Inspect the repository:*
```bash
git clone (https://github.com/Sys-tem-guy/production-workflow-lab.git)
cd production-workflow-lab
```
2. *Verify Commit History:*
```bash
git log --hraph --oneline --decorate
```
3. *Verify Health Check Utility:*
```bash
./healthcheck.sh
```

## 🛡️️ DevOps Takeaways & Best Practices
- *Branch Isolation:* Direct pushes to main are restricted, mitigating untested regressions in production.

- *Clean History:* Fast-forward merges and strict branch deletion prevent repository bloat and simplify root-cause analysis during post-mortems.

- *Observability Readiness:* Delivering standalone health check endpoints enables rapid integration with container orchestrators (e.g., Kubernetes liveness/readiness probes or Docker health checks).

---