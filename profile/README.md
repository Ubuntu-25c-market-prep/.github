# Platform Engineering Program

A greenfield AWS internal developer platform on EKS, built by 16 people across 15
workstreams.

## How the work is organised

Epics live in [`ops-program`](https://github.com/Ubuntu-25c-market-prep/ops-program) and
own their tasks as cross-repository sub-issues. Everything is tracked on the
[Platform Build board](https://github.com/orgs/Ubuntu-25c-market-prep/projects/1).

Conventions — repository, branch, commit, issue, AWS resource and Kubernetes naming — are
in [`ops-program/CONVENTIONS.md`](https://github.com/Ubuntu-25c-market-prep/ops-program/blob/main/CONVENTIONS.md).

## Repositories

| Repo | What lives there |
|---|---|
| [`infra-aws`](https://github.com/Ubuntu-25c-market-prep/infra-aws) | Terraform: AWS Org, IAM Identity Center, VPC, EKS, ECR, Bedrock |
| [`infra-modules`](https://github.com/Ubuntu-25c-market-prep/infra-modules) | Reusable, tag-versioned Terraform modules |
| [`platform-addons`](https://github.com/Ubuntu-25c-market-prep/platform-addons) | Core addons, Karpenter, KEDA, utils, Velero, Rancher, Istio |
| [`platform-observability`](https://github.com/Ubuntu-25c-market-prep/platform-observability) | Prometheus, Grafana, EFK, OpenTelemetry, Jaeger, Kubecost |
| [`platform-security`](https://github.com/Ubuntu-25c-market-prep/platform-security) | Kyverno, Policy Reporter, ZeroTrust |
| [`gitops-flux`](https://github.com/Ubuntu-25c-market-prep/gitops-flux) | Flux desired state — platform apps |
| [`gitops-argocd`](https://github.com/Ubuntu-25c-market-prep/gitops-argocd) | Argo CD and Argo Workflows — business apps |
| [`apps-business`](https://github.com/Ubuntu-25c-market-prep/apps-business) | Business application source |
| [`ops-program`](https://github.com/Ubuntu-25c-market-prep/ops-program) | Epics, backlog manifest, ADRs, runbooks |

## Workstreams

`infra` · `security` · `scaling` · `argocd` · `flux` · `monitoring` · `logging` ·
`tracing` · `utils` · `velero` · `rancher` · `finops` · `istio` · `zerotrust` · `bedrock`

Each has a GitHub team, a CODEOWNERS path, and an epic. Work is sequenced in waves: the
landing zone gates the cluster, the cluster gates Flux, Flux gates every add-on, and Istio
gates ZeroTrust.

## Working agreements

- `main` is protected everywhere. One approving review, CODEOWNERS required.
- Branches are `<type>/<issue-number>-<slug>`; commits follow Conventional Commits.
- No secrets, AWS account IDs or `.tfvars` in git. These repositories are public.
- Anything that adds AWS spend states the monthly delta in its pull request.
