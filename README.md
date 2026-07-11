# Platform Reference Knowledge Base

This repository contains platform knowledge used by the platform assistant.

The knowledge base is organized by intent:

- `standards/` contains required platform conventions and assistant behavior guidance.
- `runbooks/` contains step-by-step operational guidance for common requests.
- `examples/` contains complete reference configurations for the same-repo Helm layout.
- `policies/` describes policy expectations in human-readable form.
- `policies/kyverno/` contains Kyverno policies that the assistant should retrieve as YAML generation constraints.

The assistant indexes these documents together with configured service repositories. Search indexes are rebuildable. The live repository filesystem is authoritative for current state.

## Core Topics

- Intelligent conversation and clarification playbook
- Same-repository Helm chart and Argo CD layout
- Workload onboarding from Dockerfile or workload descriptor evidence
- Ingress / APISIX configuration inside the service Helm chart
- Resource request and limit defaults
- Kyverno policy constraints for generated YAML
- Configuration safety: local write only, no commit/push/deploy
- Common request handling (`deploy`, `apisix`, `what can you do`, `where does this go`)

## Local MVP Layout

Preferred evidence-backed layout:

```text
charts/<service>/
  Chart.yaml
  values.yaml
  templates/
argocd/<service>.yaml
```

Do not invent a separate GitOps repository when only a service repository and docs repository are configured.

## Retrieval Expectations

The assistant should prefer:

1. matching live service repository files,
2. the relevant platform standard or playbook,
3. Kyverno policy constraints,
4. a runbook for procedural questions,
5. an example only when the target service does not already have a matching file.

When sources conflict, use this precedence:

1. enforced platform policy,
2. explicit policy-compliant user input,
3. platform standards and configured defaults,
4. matching live repository conventions,
5. generic examples.

## Re-index After Changes

From `platform-assistant-agent`:

```bash
uv run platform-assist index --vector
```
