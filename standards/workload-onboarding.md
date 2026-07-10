# Workload Onboarding Standard

## Purpose

This standard defines the minimum information and Kubernetes resources required to onboard a containerized service to the platform.

## Required Workload Facts

Before generating deployment configuration, the following facts must be known:

- a DNS-compatible service name,
- a container image with an explicit tag or digest,
- the container port exposed by the workload.

The assistant must retrieve these facts from the request or the current service repository. If a required fact is absent, it must ask the service owner rather than infer the value from model knowledge.

## Optional Repository Descriptor

A repository without deployment configuration may declare its workload facts in:

```text
platform/workload.yaml
```

```yaml
apiVersion: platform-assistant.io/v1alpha1
kind: Workload
metadata:
  name: <service-name>
spec:
  image: <repository>:<explicit-tag>
  containerPort: <port>
```

This descriptor is assistant input and is not submitted to Kubernetes. Values found here count as live repository evidence and remove unnecessary clarification questions.

## Platform Defaults

Unless the request or an existing service configuration provides a compliant value:

- use one replica,
- use the service name as the Kubernetes namespace,
- expose the container port through a ClusterIP Service on the same port,
- use the service name in `app.kubernetes.io/name` labels,
- add a TCP readiness probe on the container port,
- apply the resource standard and all retrieved policy constraints.

## Required Resources

A standard service onboarding produces:

- one Helm chart,
- one Kubernetes Deployment template,
- one Kubernetes Service template,
- one Argo CD Application definition.

Ingress is optional and must be generated only when the user requests external HTTP routing.

## Safety

Generated files may be written locally only after explicit user confirmation. The onboarding workflow must not commit, push, build an image, access a cluster, or synchronize Argo CD.

## Assistant Retrieval Hints

Requests containing `deploy`, `onboard`, `bootstrap`, `create service`, `new service`, `deployment configuration`, or `make deployment configs` should retrieve this standard.
