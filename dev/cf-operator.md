# CF Operator / Project Quarks

The [CF operator] is the underlying generic tool to deploy a (modified)
BOSH deployment like Kubecf for use.

[CF operator]: https://github.com/cloudfoundry-incubator/cf-operator

It has to be installed in the same kube cluster Kubecf will be deployed to.

Installation can be done from a
[checkout](#installation-from-checkout) or from a
[release](#installation-from-release).

__Attention__: When reporting issues with Kubecf the revision of the
operator (commit hash) used to deploy it is important and necessary
information to help with reproduction.

## Installation From Release

Invoke a command like:

```shell
helm install --name cf-operator \
     --set "operator.watchNamespace=scf" \
     https://s3.amazonaws.com/cf-operators/helm-charts/cf-operator-v0.4.1%2B92.g77e53fda.tgz
```

Note that the CF-Operator can be installed in a separate namespace:

```shell
helm install --namespace cfo ...
```

This form of deployment enables restarting the operator, because it is
not affected by webhooks. It further enables the deletion of the
Kubecf deployment namespace to start from scratch, without redeploying
the operator itself.

## Installation From Checkout

### Build cf-operator

In the `cf-operator` checkout, build the image by invoking:

```sh
SAVE_TARBALL=true make build-image
```

### Install cf-operator

Load the cf-operator into the cluster, depending on if you're using
`kind` or `minikube`:

#### When using `kind`

```sh
kind load image-archive --name scf binaries/cf-operator-image.tgz
```

#### When using `minikube`

```sh
(eval $(minikube docker-env) ; docker load --input binaries/cf-operator-image.tgz)
```

#### Install cf-operator after loading

Run the following commands to run `cf-operator` _locally_, taking to your
kubernetes cluster:

```sh
export CF_OPERATOR_NAMESPACE=scf

kubectl create namespace $CF_OPERATOR_NAMESPACE

# Get the default network device, being the word after "dev".
DEFAULT_NET_DEVICE="$(ip route list 0/0 | perl -n -e '/\bdev\s+(\S+)/ && print $1')"

# Get the IP address of that device.
DEFAULT_NET_ADDR="$(ip -4 -o addr show dev "${DEFAULT_NET_DEVICE}" | perl -n -e '/\binet\s+([^\/]+)/ && print $1')"

# Deploy cf-operator.
CF_OPERATOR_WEBHOOK_SERVICE_HOST="${DEFAULT_NET_ADDR}" SKIP_IMAGE=true make up
```

As with a chart the operator can be deployed into a separate
namespace, by setting the environment variables
`CF_OPERATOR_NAMESPACE` and `WATCH_NAMESPACE` accordingly.
