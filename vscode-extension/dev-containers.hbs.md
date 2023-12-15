# Use development containers to make a development environment (alpha)

This topic tells you about using development containers (sometimes shortened to dev containers) to
make a ready-to-code development environment. This enables you to connect to a pre-configured
development container that includes all Tanzu tools and IDE extensions required for development on
Tanzu pre-installed.

> **Caution** Support for development containers is in alpha testing. It is intended for evaluation
> and test purposes only.

## <a id="overview"></a> Overview of development containers

A development container enables you to use a container as a full-featured development environment.
You can use it to:

- Run an application
- Separate tools, libraries, and runtime environments needed for working with a codebase
- Aid in continuous integration and testing

For more information, see the [Development Containers](https://containers.dev/) documentation.

## <a id="prerequisites"></a> Prerequisites

Obtain the following:

- [Docker Desktop v2.0 or later](https://www.docker.com/products/docker-desktop/) or
  [Rancher Desktop](https://rancherdesktop.io/) on Windows or macOS. If using Docker Desktop, ensure
  that you meet the [system requirements](https://code.visualstudio.com/docs/devcontainers/containers#_system-requirements)
  for the VS Code Dev Containers extension.
- The VS Code [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers).
- AMD architecture, because ARM, such as Apple M1 Silicon, is not currently supported.

## <a id="new-or-old-proj"></a> Create a new project or open an existing one

You can start a new project with support for development containers or you can add support for
development containers to an existing project:

New project
: To set up a new project by using accelerators and development containers:

   1. From the Accelerator page in Tanzu Developer Portal, select the Tanzu Java Web App accelerator.
   2. Select the options you want.
   3. Select the check box for **Include .devcontainer.json (amd64 support only)**.
   4. Open a project in VS Code.
   5. Follow the VS Code prompts to restart the IDE in `devcontainer` to connect to the development
      container.

Existing project
: To add a development container to an existing project:

   1. Open the project with VS Code and ensure that the Tanzu Developer Tools for VS Code plug-in
      is v1.1.0 or later.
   2. Create an empty new file named `devcontainer`.
   3. Type `tanzu devcontainer` and press Enter.
   4. Rename the file as `.devcontainer.json`.
   5. Follow the Visual Studio Code prompts to restart the IDE in `devcontainer` to connect to the
    development container.

## <a id="connect-to-cluster"></a> Connect to your cluster

When you start working in your development container for the first time, you must log in and
connect to your Tanzu Kubernetes cluster. The method for doing so depends on your cloud provider.
For example, for Google Cloud you might run a command similar to:

```console
gcloud container clusters get-credentials ${your_cluster_name} --region ${your_region} \
--project ${your_google_cloud_project_name}
```

For how to connect to a cluster, see the documentation for your specific cloud provider.
Examples:

- [Azure Kubernetes Service documentation](https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli#connect-to-the-cluster)
- [Amazon Elastic Kubernetes Service documentation](https://docs.aws.amazon.com/eks/latest/userguide/create-cluster.html)
- [Google Kubernetes Engine documentation](https://cloud.google.com/kubernetes-engine/docs/how-to/cluster-access-for-kubectl)

## <a id="restart-the-ide"></a> Restart the IDE

After you log in to the cluster, restart the IDE for it to detect the new cluster connection.
Press CTRL+SHIFT+P (CMD+SHIFT+P on macOS) and click **Developer: Reload Window** in the command
palette.

You are now ready to start working on your code, deploy it to your cluster, and monitor your
workloads in the Tanzu Panel. To continue your development with Tanzu Developer Tools for VS Code,
see [Use Tanzu Developer Tools for VS Code](using-the-extension.hbs.md).

## <a id="use-mounts"></a> (Optional) Use local file mounts

Use the `mounts` property in the `.devcontainer.json` file to add a volume bound to any local
directory. This is useful for sharing your Kubernetes cluster credentials with the development
container, such as a macOS or Linux host.

For example:

```console
"mounts": [
        "source=${localEnv:HOME}/.kube/,target=/home/vscode/.kube/,type=bind,consistency=cached"
    ],
```

For more information about using mounts with development containers, see the
[Visual Studio Code documentation](https://code.visualstudio.com/remote/advancedcontainers/add-local-file-mount).

## <a id="cli-eula"></a> VMware General Terms and other legal requirements connected to Tanzu CLI

When the `devcontainer` is created for the first time you are prompted to review and agree with the
[VMware General Terms](https://www.vmware.com/vmware-general-terms.html) and to participate in the
Customer Experience Improvement Program (CEIP).

The selections you make are stored and you will not prompted again when you next start
`devcontainer`.
