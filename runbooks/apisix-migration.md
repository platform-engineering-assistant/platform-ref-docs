# APISIX Migration Runbook

## Purpose

This runbook describes how to move a service from an NGINX ingress convention to the APISIX ingress convention.

## Migration Steps

1. Find the service Helm values file (`charts/<service>/values.yaml`). For legacy multi-environment overlays, use `config/<environment>/values.yaml` when that file exists.
2. Check whether an `ingress` block already exists.
3. Change `ingress.className` to `apisix` while preserving annotations, TLS, and existing hosts/paths.
4. Keep the existing host unless the platform standard requires a new host.
5. Confirm the Argo CD application already points at the service chart (or the expected environment values path for legacy layouts).
6. Produce a patch for review.

## Expected Patch Scope

Most migrations should update only the service repository values file under `charts/<service>/`.

The GitOps / Argo CD application should be changed only when:

- the application file is missing,
- the source path points to the wrong chart or environment overlay,
- the destination namespace is wrong,
- the platform standard has changed the application layout.

## Assistant Retrieval Hints

Requests containing `migrate`, `migration`, `nginx to apisix`, `change ingress controller`, or `switch ingress` should retrieve this runbook.
