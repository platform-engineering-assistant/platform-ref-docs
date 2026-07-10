# Resource Standard

## Purpose

This standard defines the default CPU and memory expectations for services deployed through the platform.

## Default Values

Services should define both requests and limits.

Recommended starting point for a small HTTP service:

```yaml
resources:
  requests:
    cpu: 100m
    memory: 128Mi
  limits:
    cpu: 100m
    memory: 128Mi
```

## Service Repository Responsibility

Resource settings belong in the Helm values used by the workload. Depending on the selected repository layout, this is either the chart's default values or an environment-specific values file.

```text
charts/<service-name>/values.yaml
# or
config/<environment>/values.yaml
```

The enforced `equal-resource-requests-limits` policy takes precedence over examples or older repository values.

## Assistant Retrieval Hints

Requests containing `cpu`, `memory`, `resource`, `limit`, `request`, or `capacity` should retrieve this standard.
