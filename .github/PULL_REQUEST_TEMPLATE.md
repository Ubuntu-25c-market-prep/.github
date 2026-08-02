<!--
Title must follow Conventional Commits with the workstream as scope:
  feat(scaling): add Graviton Spot NodePool with consolidation
-->

## What changed

<!-- One or two sentences. What a reviewer needs to know before reading the diff. -->

## Why

<!-- The problem this solves. Link the epic if the context lives there. -->

Closes #

## Verification

<!-- What you actually ran, and what it showed. Not what you intend to run. -->

- [ ] `terraform plan` reviewed / manifests rendered and diffed
- [ ] Applied to a cluster or account and observed working
- [ ] No secrets, AWS account IDs, or `.tfvars` in the diff

## Cross-workstream impact

<!-- Does this change an interface another workstream depends on? Name the workstream. -->

- [ ] None
- [ ] Affects: `<workstream>` — notified in the issue

## Cost

<!-- Anything that adds AWS spend: nodes, NAT, endpoints, load balancers, storage,
     retention. State the expected monthly delta, or "none". -->
