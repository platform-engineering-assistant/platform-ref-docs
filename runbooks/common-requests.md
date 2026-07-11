# Common Request Runbook

## Purpose

Operational guidance for frequent natural-language requests in the local Platform Assistant MVP.

## "Deploy my app" / "I need to deploy a new app"

1. List configured service repositories from application settings.
2. Ask which repository to bootstrap if the user did not name one.
3. Read live repository evidence (`Dockerfile`, `platform/workload.yaml`, existing charts).
4. Ask only for missing tagged image or container port.
5. Propose files under `charts/<service>/` and `argocd/<service>.yaml`.
6. Wait for confirmation before writing.

## "Add APISIX" / "Add ingress"

1. Confirm the service Helm chart exists.
2. Target `charts/<service>/values.yaml`.
3. Set:

```yaml
ingress:
  enabled: true
  className: apisix
  hosts:
    - host: <service>.example.internal
      paths:
        - path: /
          pathType: Prefix
```

4. Ensure `charts/<service>/templates/ingress.yaml` exists.
5. Do not create `config/dev/values.yaml` and do not invent a GitOps repository.

## "Increase memory / CPU / replicas"

1. Confirm the target service (use the remembered service when already set).
2. If Helm charts already exist, this is a configure change — not a new bootstrap.
3. Patch `charts/<service>/values.yaml` (`resources.requests`, `resources.limits`, or `replicaCount`).
4. Prefer platform default quantities from settings/evidence when the user does not specify exact values.
5. Do not refuse with "already has deployment configuration"; that only means onboarding is done.

## "Create a new repo" / unconfigured service name

Refuse. Explain that only repositories listed in `platform-assistant.yaml` are available, and that the assistant does not create Git repositories.

## "What can you do?"

Explain supported actions from configuration-safety and workload-onboarding standards:

- inspect configured repositories,
- retrieve platform standards and policies,
- bootstrap or modify Helm/Argo CD configuration,
- show evidence and diffs,
- write local files only after confirmation.

Explicitly exclude commit, push, cluster deploy, and repository creation.

## "Where will this change go?"

Answer with the concrete repository name and relative paths from the proposal. For the local MVP the answer is almost always inside the service repository under `charts/` and optionally `argocd/`.

## Assistant Retrieval Hints

Requests containing `deploy`, `apisix`, `ingress`, `memory`, `cpu`, `replica`, `capabilities`, `where`, `which file`, or `how do I` should retrieve this runbook.
