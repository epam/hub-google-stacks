# Cloud Composer

This sandbox will deploy a [Cloud Composer](https://cloud.google.com/composer)

List of the components used in this sandbox:

* [`Network`](https://github.com/agilestacks/google-components/tree/main/gke-gcloud)
* [`Cloud Composer Environment`](https://github.com/agilestacks/google-components/tree/main/composer-environment)

> Note: additional how-to information is available in [Cloud Composer Guide](https://cloud.google.com/composer/docs/how-to)

## Setup

>NOTE: If you want to undeploy or update an existing sandbox please proceed directly to Step 3 - [Recover](#recover)

First you need initialize the sandbox configuration.
To do this please run the initialization command:

```bash
hub stack init
```

The command will prompt you to enter the `GCP project ID` and
will create initial configuration files and download required components.

By default command enable auto configure of sandbox during `deploy` or `undeploy`.

### Advanced use case

For some advanced cases you need to configure sandbox manually.
To do this just pass `--disable-auto-configure` flag:

```bash
hub stack init --disable-auto-configure
```

And after that to configure sandbox manually run command:

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

If you want to change environemnt configuration and redeploy a composer environment run following command:

```bash
hub stack undeploy -c "composer"
```

Make a change in the sandbox configuration or in the body of the component and run next command:

```bash
hub stack deploy -c "composer"
```

> Note: even in minimal configuration it will still take 20+ minutes to redeploy

## Undeploy Sandbox

To delete the sandbox, run the followng command:

```bash
hub stack undeploy
```

## Parameters

Each `component` has a set of parameters (key-value pairs) such as
GKE cluster name or number of nodes in a node pool, etc.

Please explore `parameters` section of the `hub.yaml` to see what parameters are available.
Any default value can be overridden.
To get more information on how components are implemented refer to their README files.

| Name      | Description | Default Value |
| :-------- | :--------   | :-------- |
| `gke.nodeCount` | Number of GKE nodes for compose environment. Must be at least `3` | `3` |
| `gke.machineType` | Number of GKE nodes for compose environment | `n1-standard-1` |
| `composer.version` | Version of composer (`v1` or `v2`) when `v2` | `v1` |
| `component.network.subnetworkCidr` | Target environment subnet address range | `10.127.0.0/20` |

You can read about configuration options here: <https://cloud.google.com/composer/docs/how-to/managing/creating>

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

## Getting deployment result

After successful deployment you will get three URLs

1. Airflow URL
2. GCS bucket
3. GKE Cluster

You can also find it by running command:

```bash
hub show
```

If you want to see only the configuration parameters used by Composer run the following command

```bash
hub show -c "composer"
```

### Get GKE kubeconfig

Use a query string for

```bash
cluster_name="$(hub show -q '.parameters.composer.gkeCluster' -- -Mr)"
gcloud container clusters get-credentials "$cluster_name"

# to confirm cluster setup
k cluster-info
```

> TODO: we may want to delegate this to the `composer` component `post-deploy`. Depends if we bother to deploy on top anything else, (i.e. Ingress Controller, user apps etc as set of components)

## See also

* [Cloud Composer Guide](https://cloud.google.com/composer/docs/how-to)
* [Creating Environment](https://cloud.google.com/composer/docs/how-to/managing/creating)

[Hub CLI]: https://superhub.io
