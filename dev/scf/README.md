# Kubecf

## Requisites

The main [Development README](../README.md) explains the prequisites,
and how to fulfil them.

## Overview

This directory contains the bazel definitions and supporting scripts
to run Kubecf from the checkout on some kube cluster. This can be the
cluster referenced by `~/.kube/config`, or a cluster referenced by
`KUBECONFIG`.

This is in contrast to running Kubecf from a released chart.
An example of the latter would be

```
helm install \
    --namespace scf \
    --name scf https://scf-v3.s3.amazonaws.com/scf-3.0.0-82165ef3.tgz \
    --set "system_domain=scf.suse.dev" \
    --set "features.eirini=true"
```

## Targets

### Deploy Kubecf

```shell
bazel run //dev/scf:apply
```

Note that while any `*values.yaml` files in this directory are ignored
by git, they are used by Bazel to render the generated Kubecf chart
before applying it to the cluster with kubectl.

### Drop a Kubecf deployment

```shell
bazel run //dev/scf:delete
```

## Notes

The targets defined in this directory are used to generate and apply a
rendered Helm template to a Kubernetes cluster.

The [docs](./docs/) sub-directory contains more details. Start with
[Installing SCF](./docs/installing.md).
