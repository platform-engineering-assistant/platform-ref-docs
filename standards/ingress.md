# Ingress Standard

## Purpose

This standard defines how HTTP ingress should be configured for services deployed through the platform.

## Required Convention

Services that expose HTTP traffic in the `dev` or `tst` environments must use the APISIX ingress class.

Expected Helm values:

```yaml
ingress:
  enabled: true
  className: apisix
  hosts:
    - host: <service-name>.<environment>.example.internal
      paths:
        - path: /
          pathType: Prefix
```

## Service Repository Responsibility

The service repository owns the environment-specific Helm values file, such as:

```text
config/<environment>/values.yaml
```

Ingress settings should be added to that file when the service needs to expose HTTP traffic.

## GitOps Repository Responsibility

The GitOps repository owns the Argo CD `Application` resource for the service and environment.

If an application definition already exists for the service, ingress changes normally do not require creating a new Argo CD application file.

## Assistant Retrieval Hints

Requests containing `ingress`, `apisix`, `nginx`, `route`, `host`, or `expose service` should retrieve this standard.
