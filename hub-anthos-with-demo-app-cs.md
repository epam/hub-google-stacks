# GKE Sandbox Stack

## Description

GKE Sandbox stack with Anthos Service Mesh, ingress controller, and demo application

Click `Start` to go through the installation instructions.

## Prerequisites:

* You must be logged into your GCP account.

* Open the Google `cloudshell` using the following link:
https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://github.com/agilestacks/google-stacks&cloudshell_image=gcr.io/superhub/cloud-shell&cloudshell_tutorial=hub-anthos-with-demo-app.md

*NOTE: The next steps must be executed from within the `cloudshell`*

## Stack Configuration

Before you can deploy the stack we need to ask you for some information.

Please run the stack initialization command pointing to the `hub` manifest file:
```shell
hub stack init -f hub-anthos-with-demo-app-cs.yaml
```
The command will ask you to enter the ID of your GCP project.

Some of the components create DNS records (for easier access to the provisioned services) and some of them also need a GCS bucket to store their states.
For simplicity, we can pre-create Cloud DNS Zone and GCS bucket in your GCP project with random names.

Please run the following command to configure environment of the stack and pre-create required cloud resources (Cloud DNS Zone and GCS bucket):
```shell
hub stack configure
```

Every `component` has a set of parameters (key-value pairs) such as GKE cluster name or number of nodes in a node pool. 
Please explore `parameters` section of the [`hub-anthos-with-demo-app-cs.yaml`](https://source.cloud.google.com/superhub/stacks/+/master:hub-anthos-with-demo-app-cs.yaml) to see what parameters are available.
Any default value can be overridden.
To get more information on how the components are implemented refer to their README files.

## Stack Deployment

Run `hub stack deploy` to deploy the stack

Run `hub stack undeploy` to undeploy the stack

Run `hub stack deploy -c <name-of-the-component>` to deploy a specific component on the stack

Run `hub undeploy -c <name-of-the-component>` to undeploy a specific component on the stack

## Components

List of the components used in this stack:

* [`GKE Cluster`](https://source.cloud.google.com/superhub/stacks/+/master:components/gke-gcloud)
* [`GKE Node Pool`](https://source.cloud.google.com/superhub/stacks/+/master:components/gke-gcloud-node-pool)
* [`Anthos Service Mesh`](https://source.cloud.google.com/superhub/stacks/+/master:components/anthos-service-mesh)
* [`Anthos Ingress Gateway`](https://source.cloud.google.com/superhub/stacks/+/master:components/anthos-ingress-gateway)
* [`DNS Zone Record`](https://source.cloud.google.com/superhub/stacks/+/master:components/dns-zone-record-set)
* [`Online Boutique - Demo APP`](https://source.cloud.google.com/superhub/stacks/+/master:components/online-boutique-app)

## Parameters

TBD: List of stack params to override