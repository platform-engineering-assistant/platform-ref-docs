# Helm Service Chart Standard

## Purpose

This standard defines the generic Helm layout and values contract for a containerized service.

## Repository Layout

```text
charts/<service-name>/
  Chart.yaml
  values.yaml
  templates/
    deployment.yaml
    service.yaml
```

An ingress template may be added when ingress is requested.

## Required Values

The default values file must contain:

- `image` as a complete tagged image reference or digest,
- `replicaCount`,
- `containerPort`,
- `service.type`,
- `service.port`,
- CPU and memory requests,
- CPU and memory limits.

## Deployment Template

The Deployment must:

- use `apps/v1`,
- use matching selectors and pod labels,
- set the configured replica count,
- use the exact image from values,
- expose the configured container port,
- include a TCP readiness probe,
- include the configured resources.

## Service Template

The Service must:

- use `v1`,
- select the workload labels,
- default to `ClusterIP`,
- map `service.port` to `containerPort`.

## Assistant Retrieval Hints

Requests containing `helm`, `chart`, `values`, `deployment`, `service`, `deploy`, or `onboard` should retrieve this standard.
