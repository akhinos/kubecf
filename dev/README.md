# Development

This sub-directory contains the resources related to Kubecf development.

Contributors should read this document.

## Requirements

  - A kube cluster to deploy everything to.
    See [Kube Cluster Deployment](kube.md) for details and notes of
    setting such up.

  - Helm has to be available.
    See [Helm Installation](helm.md) for details and notes.

  - Kubecf is based on the CF-operator aka Project Quarks.
    See [CF Operator Installation](cf-operator.md) for details and notes.

## Deployment

With the requisites done [Kubecf can be deployed](scf/README.md).

## Pull Requests

The general work flow for pull requests contributing bug fixes,
features, etc. is

  - Branch or Fork the `suse/kubecf` repository, depending on
    permissions.

  - Implement the bug fix, feature, etc. on that branch/fork.

  - Submit a pull request based on the branch/fork through the github
    web interface, against master.

  - Developers will review the content of the pull request, asking
    questions, requesting changes, and generally discussing the
    submission.

  - After all issues with the request are resolved, and CI has passed
    a developer will merge it into master.

  - Note that it may be necessary to rebase the branch/fork to resolve
    any conflicts due to other PRs getting merging while the PR is in
    discussion. Such a rebase will be a change request from the
    developers to the contributor, on the assumption that the
    contributor is best suited to resolving the conflicts.

## Directories

todo

An important part of that are the resources for the deployment of kube
clusters using either Minikube or Kind as foundations.

TODO: Explain
  - cf_cli
  - cf_deployment
  - kube
  - linters
  - scf

Also, see SCF develop docs in [scf/README.md](scf/README.md).


TODO:
	deploy/helm/scf/
		assets/
		templates/

TODO:
	bosh/releases/pre_render_scripts/...
	(patches)

	bosh/releases/pre_render_scripts/*/*/*/patch_*

	bosh/releases/pre_render_scripts/README.md

/instance_groups/name=${INSTANCE_GROUP}/jobs/name=${JOB}/properties/quarks?/pre_render_scripts/${TYPE}

	type in jobs, ig_resolver, bpm

TODO:
	testing

TODO:
	rules
