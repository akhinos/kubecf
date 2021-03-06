# Kubecf pipeline

[This pipeline](https://concourse.suse.dev/teams/main/pipelines/kubecf) lints
builds and tests kubecf both with Eirini and Diego. The clusters used are
deployed with [kind](https://github.com/kubernetes-sigs/kind).

The pipeline tests the kubecf master branch as well as PRs with the tag
"Trigger: CI".

It uses [Catapult](https://github.com/SUSE/catapult) and requires at least one
[EKCP](https://github.com/mudler/ekcp) host (or a federated EKCP network) to
delegate the Kubernetes cluster creation to another machine, so the Concourse
workers can consume it.

## Deploy the pipeline

The following section describes the requirements and the steps needed to deploy
the pipeline from scratch.

### Requirements

The only requirement of this pipeline is an
[EKCP](https://github.com/mudler/ekcp) instance deployed in the network, which
the Concourse workers can reach.

EKCP is an API on top of Kind that allows the programmatic creation of
externally accessible clusters.

For more information, see also
[EKCP Deployment setup](https://github.com/mudler/ekcp/wiki/Deployment-setups)
and the [Catapult-web wiki page](https://github.com/SUSE/catapult/wiki/Catapult-web)
for a full guided setup.

To make the pipeline request new clusters from a different node, only adjust
the `EKCP_HOST` parameter on the pipelines/environment variable accordingly to
point to your new EKCP API endpoint.

## Deploy on Concourse

If you wish to deploy the pipeline on Concourse, run the following
command:

```
fly -t target set-pipeline -c pipeline.yaml -p kubecf
```
