# Environment Standard

## Purpose

This standard defines environment naming for the local MVP.

## Local MVP

The demonstration uses a single local cluster. Environment labels are optional for Helm chart changes.

When a hostname template includes `{environment}`, use `local` unless the user explicitly asks for another label.

## Service Repository Layout

Preferred layout (same-repo Helm chart):

```text
charts/<service>/values.yaml
```

Legacy multi-environment values files (`config/<environment>/values.yaml`) are not used by the local MVP.

## Assistant Retrieval Hints

Requests containing `environment`, `dev`, `tst`, `staging`, `prod`, or `local` may retrieve this standard for naming guidance only.
