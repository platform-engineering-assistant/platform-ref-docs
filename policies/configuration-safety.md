# Configuration Safety Policy

## Purpose

This document describes safe behavior expected from the assistant when generating platform configuration changes.

## Rules

- The assistant must not commit changes automatically.
- The assistant must not deploy changes automatically.
- The assistant must show evidence paths used for a generated patch.
- The assistant must state assumptions when host names, namespaces, or environment conventions are inferred.
- Prefer modifying an existing Helm values file under `charts/<service>/values.yaml` when that chart exists.
- Do not invent `config/<environment>/values.yaml` or a GitOps repository unless those paths/repos already exist in configuration and evidence.
- Kyverno policies under `policies/kyverno/` should be retrieved as generation constraints when producing YAML changes.
- A multi-file change set must be generated and checked before any target file is written.
- The assistant must request explicit confirmation before writing generated files into a local repository.
- Declining confirmation must leave every repository unchanged.
- The assistant must not run Git mutation commands, `kubectl`, Helm installation commands, or Argo CD synchronization commands.
- A deleted or missing repository file from an old search index must never be treated as current state.

## Assistant Retrieval Hints

Requests containing `patch`, `generate`, `apply`, `commit`, `deploy`, or `safe` should retrieve this policy.
