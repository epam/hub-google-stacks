# Cloud SQL with Load Test

## Description

Cloud SQL with all supported database engines.

List of the components used in this sandbox:

* [`VPC Network`](https://github.com/agilestacks/google-components/tree/main/network)
* [`Cloud SQL`](https://github.com/agilestacks/google-components/tree/main/cloud-sql)

Click `Start` to go through the sandbox installation instructions.

## Prerequisites

* You must be logged into your GCP account.

* Open the Google `cloudshell` using the following [`link`](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/agilestacks/google-stacks&&cloudshell_git_branch=main&cloudshell_image=gcr.io/superhub/cloud-shell&cloudshell_tutorial=README.md&cloudshell_open_in_editor=hub.yaml&cloudshell_workspace=cloud-sql-all-in-one)

*NOTE: The next steps must be executed from within the `cloudshell`*

## Configuration

Before you can deploy the sandbox we need to ask you for some information.

Please run the initialization command pointing to the `hub` manifest file:

```bash
hub stack init
```

The command will prompt you to enter the ID of your GCP project.

Some of the components create DNS records (for easier access to the provisioned services) and some of them also need a GCS bucket to store their states.
The tool (`hub cli`) we use to provision sandboxes itself produces a state file that must be uploaded to the cloud.
For simplicity, we can pre-create Cloud DNS Zone and GCS bucket in your GCP project with random names.

Please run the following command to configure the environment of pre-create the required cloud resources (Cloud DNS Zone and GCS bucket):

```bash
hub stack configure
```

If any of the sandbox components would require additional configuration parameters, users will be asked to provide them.

Every `component` has a set of parameters (key-value pairs) such as GKE cluster name or number of nodes in a node pool.
Please explore `parameters` section of the [`hub.yaml`](https://github.com/agilestacks/google-stacks/blob/main/cloud-sql-all-in-one/hub.yaml) to see what parameters are available.
Any default value can be overridden.
To get more information on how the components are implemented refer to their README files.

### How to recover the configuration of an existing sandbox?

Google Cloud Shell environments are ephemeral, which means any files stored locally on the Cloud Shell machine will be lost when the machine restarts. Luckily, we store sandbox state files in the Cloud, which means, if we lose a local state, we can always recover it from the Cloud.

Execute the following commands to recover a state of a sandbox:

```bash
hub stack init -s gs://{sandbox state bucket}/{stack dns domain}/hub/hub.state
hub stack configure
```

Please browse GCS buckets in your project to find the right one by the convention below:

GCS path naming convention:

*gs://{sandbox state bucket}/{stack dns domain}/hub/hub.state*

Example:

*gs://superhub-superhub/overconfident-corvo-216.epam.devops.delivery/hub/hub.state*

After state is recovered, you can undeploy or update your sandbox.

## Stack Deployment

Run to deploy the sandbox

```bash
hub stack deploy
```

Run to undeploy the sandbox

```bash
hub stack undeploy
```
