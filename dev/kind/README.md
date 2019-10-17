# Kind

## Overview

This directory contains the bazel definitions and supporting scripts
to run and develop Kubecf on a K-in-D foundation (Kube IN Docker).

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
