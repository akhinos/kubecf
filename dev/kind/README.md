# Foundation: Kube: Kind (Kube IN Docker)

## Overview

This directory contains bazel definitions and supporting scripts to
run and develop Kubecf on a KinD foundation (Kube IN Docker).

## Limitations

KinD __does not work__ with the Ingress features of the Kubecf chart.

This means that it is not possible to set a Kubecf deployment on a
KinD cluster up for external access.

This is still good enough for local development, running smoke tests,
etc.

It is important to note that the `system_domain` for Kubecf has to be
set to a value resolving to its public service cluster IP. This is
trivial to do with a DNS service like `nip.io`, `xip.io`, etc.

## Start a cluster

For developing with [kind](https://github.com/kubernetes-sigs/kind),
start a local cluster by running the `start` target:

```shell
bazel run //dev/kind:start
```

Don't forget to also set your `KUBECONFIG`:

```shell
export KUBECONFIG="$(bazel run @kind//:kind -- get kubeconfig-path --name="scf")"
```

## Tear a cluster down

Tear the entire cluster down by running the `delete` target:

```shell
bazel run //dev/kind:delete
```
