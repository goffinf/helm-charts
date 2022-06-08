## Usage

[Helm](https://helm.sh) must be installed to use the charts.  Please refer to
Helm's [documentation](https://helm.sh/docs) to get started.

Once Helm has been set up correctly, add the repo as follows:

    helm repo add <alias> https://<orgname>.github.io/helm-charts

Example:

    helm repo add gh-helm-charts https://goffinf.github.io/helm-charts

If you had already added this repo earlier, run `helm repo update` to retrieve
the latest versions of the packages.  You can then run `helm search repo
<alias>` to see the charts.

Example:

    helm search repo gh-helm-charts

    NAME                            CHART VERSION   APP VERSION     DESCRIPTION
    gh-helm-charts/nginx-hello      0.1.6           1.0             A Helm Chart to manage a deployment of the NGIN...

To install the <chart-name> chart:

    cd my-working-dir
    helm pull --untar --version <version> <alias>/<chart-name>
    helm --debug upgrade nginx-hello --values <chart-name>/values-common.yaml --values <chart-name>/a-n-other-values.yaml ./<chart-name> --version <version> --namespace=<k8s-namespace> --install --force [--dry-run]

Example:

    helm pull --untar --version 0.1.6 gh-helm-charts/nginx-hello
    helm --debug upgrade nginx-hello --values nginx-hello/values-common.yaml --values nginx-hello/values-k3d-ci.yaml ./nginx-hello --version 0.1.6 --namespace=default --install --force --dry-run
  
To uninstall the chart:

    helm uninstall <chart-name>

Example:
    
    helm ls

    NAME            NAMESPACE       REVISION        UPDATED                                 STATUS          CHART                   APP VERSION
    nginx-hello     default         1               2022-06-08 19:28:28.2378383 +0100 BST   deployed        nginx-hello-0.1.6       1.0

    helm uninstall nginx-hello
    
    release "nginx-hello" uninstalled
