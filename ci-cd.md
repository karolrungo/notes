---
title: CI/CD - Continuous Integration & Delivery
created: 2026-05-14
tags: [devops, ci-cd, fundamentals, pipelines]
aliases: [CI/CD, Continuous Integration, Continuous Delivery]
---

# CI/CD — Continuous Integration & Delivery

> [!summary] TL;DR
> - **CI** = auto-build + test every commit, keep `main` green.
> - **CD** = auto-package every green build into a deployable artifact (**Delivery**) or deploy it straight to prod (**Deployment**).
> - **Pipeline** = the codified path from commit to production.

---

## CI — Continuous Integration

Practice of frequently merging code from all developers into a shared mainline branch (`main`), where each push triggers an automated **build → test → static analysis** sequence.

**Key properties:**
- Devs commit small changes **multiple times per day**.
- Failing build/tests **block the merge**.
- `main` must always be in a **buildable, releasable state**.
- Catches integration bugs early, when they're cheapest to fix.
- Prevents long-lived branches and "merge hell".

**Tooling:** GitHub Actions, GitLab CI, Jenkins, CircleCI, Buildkite, Bazel + remote cache.

Related: [[Trunk-Based Development]], [[Code Review]]

---

## CD — Continuous Delivery vs Continuous Deployment

Often confused — they are **not** the same.

|                 | Continuous **Delivery**   | Continuous **Deployment**                   |
| --------------- | ------------------------- | ------------------------------------------- |
| Pipeline output | Release-ready artifact    | Live production deploy                      |
| Final step      | **Manual** approval       | **Fully automated**                         |
| Risk profile    | Lower (human gate)        | Higher (needs strong tests + observability) |
| Common in       | Regulated / infra changes | Mature SaaS web apps                        |

**Core principle:** *Build once, deploy many* — the same immutable artifact is promoted through dev → staging → prod.

---

## CI/CD Pipeline

```
Commit → Build → Test → Package → Security → Deploy → Verify → (Rollback?)
```

| Stage | Purpose | Example tools |
|---|---|---|
| **Source** | Git push triggers webhook | GitHub, GitLab |
| **Build** | Compile / build container image | Bazel, Gradle, Docker |
| **Test** | Unit, integration, contract, E2E | JUnit, pytest, Playwright |
| **Static analysis** | Lint, type-check, SAST | `tflint`, `terraform validate`, golangci-lint |
| **Package** | Push artifact to registry | Artifact Registry, GHCR, ECR |
| **Security** | Image scan, SBOM, CVE check | Trivy, Grype, Snyk |
| **Deploy** | Roll out to environment | ArgoCD, Helm, Terraform |
| **Verify** | Smoke tests, health probes, SLOs | Prometheus, Datadog |
| **Rollback** | Auto-revert on failure | Argo Rollouts, Flagger |

### Deployment Strategies

- **Rolling update** — replace pods N at a time (k8s default).
- **Blue/Green** — run two envs in parallel, flip traffic.
- **Canary** — route small % of traffic, monitor, expand.
- **Feature flags** — decouple **deploy** from **release**.

---

## CI/CD for Infrastructure (Terraform)

```
PR opened
  ├─ terraform fmt -check
  ├─ terraform validate
  ├─ tflint
  ├─ terraform plan      → posted as PR comment
  └─ policy checks
       │
  PR approved + merged
       │
       ▼
  terraform apply        ← human-gated
       │
       ▼
  Post-apply health checks (pods, DB, restarts)
```

**Key differences vs app pipelines:**
- `plan ≠ apply` — plans are safe in PRs; applies mutate real infra.
- **State locking** is critical (no concurrent applies).
- **Drift detection** runs on a schedule.
- Blast radius is much larger → stronger approval gates.

Related: [[Terraform State Management]], [[GitOps]]

---

## Core DevOps Principles That Make CI/CD Work

1. **Trunk-based development** — short-lived branches.
2. **Everything as code** — app, infra, config, pipelines.
3. **Immutable artifacts** — build once, promote unchanged.
4. **Environment parity** — same shape, different scale. (dev / pre / prod)
5. **Fast feedback** — keep pipelines under ~10 min.
6. **Observability** — you can't deploy what you can't measure.
7. **Automated rollback** — recovery must be as automated as deploy.

---

## Anti-Patterns to Avoid

> [!warning] Common mistakes
> - Long-lived feature branches → defeats the "integration" in CI.
> - Skipping tests "just this once".
> - Manual steps hidden in the pipeline (snowflake builds).
> - Mutable image tags (`:latest`) → breaks reproducibility.
> - Deploying on Friday afternoon with no rollback plan.
> - Treating "green pipeline" as "working software" — verify in production.

---

## See Also

- [[GitOps]]
- [[Trunk-Based Development]]
- [[Terraform Workflow]]
- [[Observability Basics]]
- [[Deployment Strategies]]