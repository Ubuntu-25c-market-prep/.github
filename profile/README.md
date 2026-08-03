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

One repository per **delivery boundary** — something that changes how or when code
reaches production — rather than one per component. See
[ADR 0010](https://github.com/Ubuntu-25c-market-prep/ops-program/blob/main/docs/adr/0010-one-repository-per-delivery-boundary.md).

| Repo | What lives there | Delivered by |
|---|---|---|
| [`infra-aws`](https://github.com/Ubuntu-25c-market-prep/infra-aws) | Terraform: AWS Org, IAM Identity Center, VPC, EKS, ECR, Bedrock, plus `modules/` | Terraform, CI apply role |
| [`gitops-flux`](https://github.com/Ubuntu-25c-market-prep/gitops-flux) | Platform add-ons, observability and security, and the Flux objects that deliver them | Flux |
| [`gitops-argocd`](https://github.com/Ubuntu-25c-market-prep/gitops-argocd) | Business app delivery config — ApplicationSets, promotion path | Argo CD |
| [`apps-business`](https://github.com/Ubuntu-25c-market-prep/apps-business) | Business application source and its image pipeline | CI, into ECR |
| [`ops-program`](https://github.com/Ubuntu-25c-market-prep/ops-program) | Epics, backlog manifest, ADRs, runbooks | not delivered |
| [`.github`](https://github.com/Ubuntu-25c-market-prep/.github) | This profile, the shared security workflow, issue and PR templates | reusable workflow |

`infra-modules`, `platform-addons`, `platform-observability` and `platform-security`
were archived by ADR 0010 and their contents moved into the repositories above.
Their issues remain readable.

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
