# Platform Reference Knowledge Base

This repository contains platform knowledge used by the platform assistant.

The knowledge base is organized by intent:

- `standards/` contains required platform conventions.
- `runbooks/` contains step-by-step migration or operational guidance.
- `examples/` contains complete reference configurations.
- `policies/` describes policy expectations in human-readable form.
- `policies/kyverno/` contains Kyverno policies that the assistant should retrieve as YAML generation constraints.

The assistant indexes these documents together with service repositories and GitOps repositories. A service-team request should retrieve only the documents relevant to the requested application, environment, resource, and platform technology.

## Core Topics

- Ingress configuration and APISIX migration
- Service onboarding through GitOps
- Resource request and limit defaults
- Kyverno policy constraints for generated YAML
- Environment naming conventions
- Argo CD application layout
- Lower-environment GitOps layout for `dev` and `tst`
- Generic workload onboarding from an empty deployment configuration
- Same-repository Helm and Argo CD layout

## Retrieval Expectations

The assistant should prefer:

1. a matching service repository configuration,
2. a matching GitOps application definition,
3. the relevant platform standard,
4. an example only when the target service does not already have a matching file,
5. a runbook when the request is about migration or change procedure.

When sources conflict, use this precedence:

1. enforced platform policy,
2. explicit policy-compliant user input,
3. platform standards and configured defaults,
4. matching live repository conventions,
5. generic examples.

The live repository filesystem is authoritative for current state. Search indexes are rebuildable retrieval data and must not preserve deleted files as current evidence.
