# Repository Layout Standard

## Purpose

This standard defines supported locations for deployment configuration without requiring a particular application name or repository topology.

## Same-Repository Layout

The preferred layout for a small service or local demonstration is:

```text
charts/<service-name>/
argocd/<service-name>.yaml
```

The Helm chart and Argo CD Application are stored beside the service source or in an otherwise dedicated service repository. No separate GitOps repository is required.

## Split-Repository Layout

Platforms that separate application and deployment ownership may instead use:

```text
service repository: config/<environment>/values.yaml
GitOps repository:  apps/<environment>/<service-name>.yaml
```

The assistant must select a layout from current repository evidence and configured repository roles. It must not invent a second repository when only a service repository is configured.

## Assistant Retrieval Hints

Requests containing `repository`, `layout`, `deploy`, `gitops`, `argocd`, `chart`, or `environment` should retrieve this standard.
