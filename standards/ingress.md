# Ingress Standard

## Purpose

This standard defines how HTTP ingress should be configured for services deployed through the platform.

## Required Convention

Services that expose HTTP traffic use the APISIX ingress class.

Expected Helm values in `charts/<service>/values.yaml`:

```yaml
ingress:
  enabled: true
  className: apisix
  hosts:
    - host: <service-name>.example.internal
      paths:
        - path: /
          pathType: Prefix
```

The chart must also include `charts/<service>/templates/ingress.yaml` that renders when `ingress.enabled` is true.

## Service Repository Responsibility

The service repository owns the Helm chart and optional Argo CD Application file:

```text
charts/<service>/
  Chart.yaml
  values.yaml
  templates/
    deployment.yaml
    service.yaml
    ingress.yaml
argocd/<service>.yaml
```

Ingress settings are added to the chart values file. There is no separate GitOps repository in the local MVP.

## Assistant Retrieval Hints

Requests containing `ingress`, `apisix`, `nginx`, `route`, `host`, or `expose service` should retrieve this standard.
