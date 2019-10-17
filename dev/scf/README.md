# Kubecf

## Overview

This directory contains the bazel definitions and supporting scripts
to run Kubecf from the checkout on some kube cluster. This can be the
cluster referenced by `~/.kube/config`, or a cluster referenced by
`KUBECONFIG`.

This is in contrast to running Kubecf from a released chart.

## Foundations

See the sibling directories [minikube](../minikube/) and
[kind](../kind/) for ways of starting a local cluster based on
Minikube or Kind.

## Deploy Kubecf

```shell
bazel run //dev/scf:apply
```

Note that while any `*values.yaml` files under this directory are
ignored by git, they are used by Bazel to render the Kubecf chart
before applying to the cluster with kubectl.

## Drop a Kubecf deployment

```shell
bazel run //dev/scf:delete
```

## Notes

The targets defined in this directory are used to generate and apply a
rendered Helm template to a Kubernetes cluster.

The [docs](./docs/) sub-directory contains more details. Start with
[Installing SCF](./docs/installing.md).
