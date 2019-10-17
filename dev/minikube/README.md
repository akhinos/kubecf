# Minikube

## Overview

This directory contains the bazel definitions and supporting scripts
to run and develop Kubecf on a Minikube foundation.

IMPORTANT! The `~/.kube/config` file will be edited by Minikube. Make
a backup if you want to preserve the original configuration.

Alternatively, set the environment variable `KUBECONFIG` to the path
of the configuration file you wish to use and Minikube will then
create and/or edit that file, leaving the global configuration
untouched.

## Start a cluster

For developing with Minikube, start a local cluster by running the
`start` target:

```shell
bazel run //dev/minikube:start
```

### Managing system resources

The following environment variables are used by the `start` target to
allocate the resources used by Minikube:

  - VM_CPUS - the number of CPUs Minikube will use.
  - VM_MEMORY - the amount of RAM Minikube will be allowed to use.
  - VM_DISK_SIZE - the disk size Minikube will be allowed to use.

E.g.:

```shell
VM_CPUS=6 VM_MEMORY=$((1024 * 24)) VM_DISK_SIZE=180g bazel run //dev/minikube:start
```

### Specifying a different Kubernetes version

Set the `K8S_VERSION` environment variable to override the default
version.

### VM Drivers

At the moment, only the VirtualBox and KVM2 drivers are working
correctly. Set the `VM_DRIVER` environment variable to override the
default. E.g. `VM_DRIVER=kvm2`.

## Tear cluster down

Tear the entire cluster down by running the `delete` target:

```shell
bazel run //dev/minikube:delete
```
