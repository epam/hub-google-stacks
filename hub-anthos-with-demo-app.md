# GKE Sandbox

## Description

GKE Sandbox with Anthos Service Mesh, ingress controller, and demo application

Click `Start` to go through the installation instructions.

## Prerequisites:

* You must be logged into your GCP account.

* Open the Google `cloudshell` using the following link (if not already opened):
https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/agilestacks/google-stacks&cloudshell_image=gcr.io/superhub/cloud-shell&cloudshell_tutorial=hub-anthos-with-demo-app.md

*NOTE: The next steps must be executed from within the `cloudshell`*

## Configuration

Before you can deploy the sandbox we need to ask you for some information.

Please run the initialization command pointing to the `hub` manifest file:
```shell
hub stack init -f hub-anthos-with-demo-app.yaml
```
The command will ask you to enter the ID of your GCP project.

Some of the components create DNS records (for easier access to the provisioned services) and some of them also need a GCS bucket to store their states.
The tool (`hub cli`) we use to provision sandboxes itself produces a state file that must be uploaded to the cloud.
For simplicity, we can pre-create Cloud DNS Zone and GCS bucket in your GCP project with random names.

Please run the following command to configure the environment of pre-create the required cloud resources (Cloud DNS Zone and GCS bucket):
```shell
hub stack configure
```
If any of the sandbox components would require additional configuration parameters, users will be asked to provide them.

Every `component` has a set of parameters (key-value pairs) such as GKE cluster name or number of nodes in a node pool. 
Please explore `parameters` section of the [`hub-anthos-with-demo-app.yaml`](https://source.cloud.google.com/superhub/stacks/+/master:hub-anthos-with-demo-app-cs.yaml) to see what parameters are available.
Any default value can be overridden.
To get more information on how the components are implemented refer to their README files.

### How to recover the configuration of an existing sandbox?

Google Cloud Shell environments are ephemeral, 
which means any files stored locally on the Cloud Shell machine will be lost when 
the machine restarts.
Luckily, we store sandbox state files in the Cloud, 
which means, if we lose a local state, we can always recover it from the Cloud.

Execute the following commands to recover a state of a sandbox:
```shell
hub stack init -f hub-anthos-with-demo-app.yaml -s {GCS path to a state file of the sanbox}
hub stack configure
```
Please browse GCS buckets in your project to find the right one by the convention below:

GCS path naming convention:

*gs://{sandbox state bucket}/{stack dns name}/hub/hub.state*

Example:

*gs://superhub-superhub/overconfident-corvo-216.epam.devops.delivery/hub/hub.state*

After state is recovered, you can undeploy or update your sandbox.

## Stack Deployment

Run `hub stack deploy` to deploy the sandbox

Run `hub stack undeploy` to undeploy the sandbox

Run `hub stack deploy -c <name-of-the-component>` to deploy a specific component on the sandbox

Run `hub undeploy -c <name-of-the-component>` to undeploy a specific component on the sandbox

## Components

List of the components used in this sandbox:

* [`GKE Cluster`](https://source.cloud.google.com/superhub/stacks/+/master:components/gke-gcloud)
* [`GKE Node Pool`](https://source.cloud.google.com/superhub/stacks/+/master:components/gke-gcloud-node-pool)
* [`Anthos Service Mesh`](https://source.cloud.google.com/superhub/stacks/+/master:components/anthos-service-mesh)
* [`Anthos Ingress Gateway`](https://source.cloud.google.com/superhub/stacks/+/master:components/anthos-ingress-gateway)
* [`DNS Zone Record`](https://source.cloud.google.com/superhub/stacks/+/master:components/dns-zone-record-set)
* [`Online Boutique - Demo APP`](https://source.cloud.google.com/superhub/stacks/+/master:components/online-boutique-app)

## Parameters

TBD: List of sandbox params to override
