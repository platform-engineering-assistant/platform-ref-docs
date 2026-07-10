# APISIX Migration Runbook

## Purpose

This runbook describes how to move a service from an NGINX ingress convention to the APISIX ingress convention.

## Migration Steps

1. Find the service repository environment values file.
2. Check whether an `ingress` block already exists.
3. Change `ingress.className` to `apisix`.
4. Keep the existing host unless the platform standard requires a new host.
5. Confirm the GitOps application already points to the expected environment values path.
6. Produce a patch for review.

## Expected Patch Scope

Most migrations should update only the service repository values file.

The GitOps repository should be changed only when:

- the application file is missing,
- the source path points to the wrong environment,
- the destination namespace is wrong,
- the platform standard has changed the application layout.

## Assistant Retrieval Hints

Requests containing `migrate`, `migration`, `nginx to apisix`, `change ingress controller`, or `switch ingress` should retrieve this runbook.

