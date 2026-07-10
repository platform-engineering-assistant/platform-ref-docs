# GitOps Application Standard

## Purpose

This standard defines how a Helm-based service is represented by Argo CD in either a same-repository or split-repository layout.

## Same-Repository Location

For a service repository that owns its Helm chart, use:

```text
argocd/<service-name>.yaml
```

Set `spec.source.path` to `charts/<service-name>`.

## Split-Repository Location

When a configured GitOps repository owns Argo CD resources, use `apps/<environment>/<service-name>.yaml` and the environment-specific source path defined by that platform.

## Required Fields

The application should define:

- `metadata.name`
- `spec.source.repoURL`
- `spec.source.targetRevision`
- `spec.source.path`
- `spec.destination.namespace`
- `spec.syncPolicy`

For a local demonstration, set `CreateNamespace=true`. The destination namespace defaults to the service name. The source repository URL and target revision must come from the current Git repository or explicit user input.

## Example Shape

```yaml
apiVersion: argoproj.io/v1alpha1
kind: Application
metadata:
  name: example-service
  namespace: argocd
spec:
  project: default
  source:
    repoURL: https://example.invalid/example-service.git
    targetRevision: main
    path: charts/example-service
  destination:
    server: https://kubernetes.default.svc
    namespace: example-service
  syncPolicy:
    automated:
      prune: true
      selfHeal: true
    syncOptions:
      - CreateNamespace=true
```

## Assistant Retrieval Hints

Requests containing `deploy`, `deployment`, `gitops`, `argocd`, `application`, `chart`, or `environment` should retrieve this standard.
