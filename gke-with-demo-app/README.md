# GKE Sandbox

## Description

GKE Sandbox with ingress controller and demo application

![Schema](https://gcp.devops.delivery/images/gke-without-anthos.png)

List of the components used in this sandbox:

* [`GKE Cluster`](https://github.com/agilestacks/google-components/tree/main/gke-gcloud)
* [`Nginx - ingress controller`](https://github.com/agilestacks/google-components/tree/main/nginx)
* [`External DNS - dns record provisioner`](https://github.com/agilestacks/google-components/tree/main/external-dns)
* [`Online Boutique - Demo APP`](https://github.com/agilestacks/google-components/tree/main/online-boutique-app)

## Setup

>NOTE: If you want to undeploy or update an existing sandbox please proceed directly to Step 3 - [Recover](#recover)

First you need initialize the sandbox configuration.
To do this please run the initialization command:

```bash
hub stack init
```

The command will prompt you to enter the `GCP project ID` and
will create initial configuration files and download required components.

Next, to configure the sandbox manually run the following command:

```bash
hub stack configure
```

The [Hub CLI] produces a state file after provisioning of sandbox,
same as its components, and it must be uploaded to the cloud.
For simplicity, we pre-create `Cloud DNS Zone` and `GCS bucket`
in your GCP project with pre-generated names.
This is done during `configure` command.

## Deploy Sandbox

Once you are done with the configuration, use the following command to deploy the sandbox:

```bash
hub stack deploy
```

To deploy a specific component on the sandbox:

```bash
hub stack deploy -c <name-of-the-component>
```

## Undeploy Sandbox

To delete the sandbox run this command:

```bash
hub stack undeploy
```

To undeploy a specific component on the sandbox:

```bash
hub stack undeploy -c <name-of-the-component>
```

## Parameters

Each `component` has a set of parameters (key-value pairs) such as
GKE cluster name or number of nodes in a node pool, etc.

Please explore `parameters` section of the `hub.yaml` to see what parameters are available.
Any default value can be overridden.
To get more information on how components are implemented refer to their README files.

## Recover

Google Cloud Shell environments are ephemeral, which means any files stored locally
on the Cloud Shell machine will be lost when the machine restarts.
Luckily, we store sandbox state files in the Cloud, which means,
if we lose a local state, we can always recover it from the Cloud.

To recover your sandbox please follow the steps below.

Switch to your current project:

```bash
gcloud config set project <project-id>
```

List all recent sandboxes deployed to your project and find ID of the sandbox you would like to recover:

```bash
hub state ls
```

Initialize your sandbox:

```bash
hub stack init <id>
```

[Hub CLI] will find the location of the state file, download it and prepare configuration files.

After stack recovery undeploy or update your existing stack using corresponding commands.

## See also

* [Demo App Source Code and Documentation](https://github.com/GoogleCloudPlatform/microservices-demo/)

## Architecture Diagram

![GKE Sandbox Architecture](https://gcp.devops.delivery/images/gke_nginx_diagram.png)

[Hub CLI]: https://superhub.io
