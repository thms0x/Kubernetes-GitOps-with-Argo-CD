# GitOps with Argo CD: Kubernetes Deployment, Promotion, and Rollback

**Team 4** — Jakub Wilk, Thomas Rafetseder, Esmin Alekic

## Description

We will build a GitOps workflow that deploys a versioned web service to Kubernetes and promotes releases from development to production through GitHub pull requests. The project will demonstrate how Argo CD keeps a running cluster in sync with Git, repairs configuration drift, and applies a rollback recorded in Git.

## Scope

- Run one local Kubernetes cluster using kind, with separate `dev` and `prod` namespaces.
- Build and containerize a Java Spring Boot HTTP service with `/version` and `/health` endpoints. Version the source code in Git and host it on GitHub.
- Keep a shared Kubernetes manifest base and two Kustomize overlays in the same GitHub repository.
- Configure one Argo CD Application per environment, with automated sync and self-healing enabled. Review production configuration changes through pull requests.

## Demo Scenarios

| Scenario | Action | Expected result |
|---|---|---|
| Deploy to development | Merge a change to the image digest in the `dev` overlay. | Argo CD applies the change. `/version` reports `v2` in `dev` and `v1` in `prod`. |
| Promote to production | Review and merge a pull request that sets the `prod` image digest to the one running in `dev`. | The `prod` application becomes healthy, and `/version` reports `v2`. The pull request records the promoted image digest. |
| Repair drift | Manually scale the `prod` Deployment from two replicas to one. | Argo CD restores the declared count of two replicas. Record how long it takes from the manual change until both replicas are ready. |
| Roll back | Revert the production promotion commit in Git. | `/version` reports `v1` in `prod` and `v2` in `dev`. Git history records both the promotion and the rollback. |

## Milestones

| Milestone | Owner | Completion criteria |
|---|---|---|
| Demo app and release images | TBA | Two container images are published with distinct digests. Their `/version` endpoints report `v1` and `v2`, respectively. |
| Cluster and GitOps integration | TBA | A fresh kind cluster runs both environments, and Argo CD reports both applications as Synced and Healthy. |
| Promotion, drift repair, and rollback | TBA | All four demo scenarios pass. The team records the observed versions, sync statuses, and drift recovery time. |
| Documentation and presentation | All team members | The team can reproduce the demo by following `README.md`. The presentation slides and speaking parts are ready. |
