# Web Server Sandbox Stack

## Description

Web Server Sandbox stack with VM, private VPC, load balancer, private Cloud SQL

Click `Start` to go through the installation instructions.

## Prerequisites

* You must be logged into your GCP account.

* Open the Google `cloudshell` using the following [`link`](https://ssh.cloud.google.com/cloudshell/editor?cloudshell_git_repo=https://source.developers.google.com/p/superhub/r/stacks&cloudshell_image=gcr.io/superhub/cloud-shell&cloudshell_tutorial=hub-vm-app.md)

*NOTE: The next steps must be executed from within the `cloudshell`*

## Stack Configuration

Before you can deploy the stack we need to ask you for some information.

Please run the stack initialization command pointing to the `hub` manifest file:

```shell
hub stack init -f hub-vm-app.yaml
```

The command will ask you to enter the ID of your GCP project.

Some of the components create DNS records (for easier access to the provisioned services) and some of them also need a GCS bucket to store their states.
For simplicity, we can pre-create Cloud DNS Zone and GCS bucket in your GCP project with random names.

Please run the following command to configure environment of the stack and pre-create required cloud resources (Cloud DNS Zone and GCS bucket):

```shell
hub stack configure
```

Every `component` has a set of parameters (key-value pairs) such as VM imagr or Cloud SQL database name or user.
Please explore `parameters` section of the [`hub-vm-app.yaml`](https://source.cloud.google.com/superhub/stacks/+/master:hub-vm-app.yaml) to see what parameters are available.
Any default value can be overridden.
To get more information on how the components are implemented refer to their README files.

## Stack Deployment

Run `hub stack deploy` to deploy the stack

Run `hub stack undeploy` to undeploy the stack

Run `hub stack deploy -c <name-of-the-component>` to deploy a specific component on the stack

Run `hub undeploy -c <name-of-the-component>` to undeploy a specific component on the stack

## Components

List of the components used in this stack:

* [`SSL Certificate`](https://source.cloud.google.com/superhub/stacks/+/master:components/certificate)
* [`VPC Network`](https://source.cloud.google.com/superhub/stacks/+/master:components/network)
* [`Cloud SQL`](https://source.cloud.google.com/superhub/stacks/+/master:components/cloud-sql)
* [`Cloud NAT`](https://source.cloud.google.com/superhub/stacks/+/master:components/cloud-nat)
* [`Managed Instance Group`](https://source.cloud.google.com/superhub/stacks/+/master:components/managed-instance-group)
* [`Load balancing`](https://source.cloud.google.com/superhub/stacks/+/master:components/load-balancer)
* [`DNS Zone Record`](https://source.cloud.google.com/superhub/stacks/+/master:components/dns-zone-record-set)

## Parameters

TBD: List of stack params to override
