# Minikube

## Overview

This directory contains bazel definitions and supporting scripts to
run and develop Kubecf on a Minikube foundation.

It is of course possible to use `minikube` commands directly, bypassing bazel.

__IMPORTANT!__ Minikube will edit the `~/.kube/config` file, or
whatever file the environment variable `KUBECONFIG` references. Make a
backup if you want to preserve the original configuration.

The alternative is of course to change the environment variable
`KUBECONFIG` to the path of the desired local configuration file and
Minikube will then create that file, leaving any other configuration
untouched.

## Start a cluster

For developing with Minikube, start a local cluster by either running
the `start` target:

```shell
bazel run //dev/minikube:start
```

or by directly invoking the `minikube` command:

```
minikube start
```

### Managing system resources

We need more disk space in minikube, otherwise pods will get evicted and the deployment will be in a constant loop.

The following environment variables are used by the `start` target to
allocate the resources used by Minikube:

  - VM_CPUS - the number of CPUs Minikube will use.
  - VM_MEMORY - the amount of RAM Minikube will be allowed to use.
  - VM_DISK_SIZE - the disk size Minikube will be allowed to use.

E.g.:

```shell
VM_CPUS=6 VM_MEMORY=$((1024 * 24)) VM_DISK_SIZE=180g bazel run //dev/minikube:start
```

When bypassing bazel resource usage can be specified on the command
line for `minikube start`:

```shell
minikube start  --memory=12000mb --cpus=4 --disk-size=40gb
```

### Specifying a different Kubernetes version

Set the `K8S_VERSION` environment variable to override the default
version.

Or use option `--kubernetes-version`:

```shell
minikube start --kubernetes-version v1.14.1
```

### VM Drivers

At the moment, only the VirtualBox and KVM2 drivers are working
correctly. Set the `VM_DRIVER` environment variable to override the
default. E.g. `VM_DRIVER=kvm2`.

## Tear cluster down

Tear the entire cluster down by either running the `delete` target:

```shell
bazel run //dev/minikube:delete
```

or by directly invoking the `minikube` command:

```
minikube delete
```
