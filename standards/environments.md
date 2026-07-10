# Environment Standard

## Purpose

This standard defines environment naming and file layout expectations.

## Environments

The prototype platform uses these environment names:

| Environment | Purpose |
| --- | --- |
| `dev` | development validation |
| `tst` | test validation |
| `staging` | pre-production validation |
| `prod` | production workloads |

## Service Repository Layout

Environment-specific Helm values should use:

```text
config/<environment>/values.yaml
```

## GitOps Repository Layout

Argo CD application definitions should use:

```text
apps/<environment>/<service-name>.yaml
```

The `platform-gitops-devtst` repository contains only the lower environments:

```text
apps/dev/<service-name>.yaml
apps/tst/<service-name>.yaml
```

## Assistant Retrieval Hints

Requests containing an environment name should retrieve matching service and GitOps files before general examples.
