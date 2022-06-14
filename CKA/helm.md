# HELM

## Chart Contents

A chart is an archived set of Kubernetes resource manifests that make up a distributed application. You can learn more from the Helm 3 documentation. Others exist and can be easily created, for example by a vendor providing software. Charts are similar to the use of independent YUM repositories.

```a
├── Chart.yaml
├── README.md
├── templates
│   ├── NOTES.txt
│   ├── _helpers.tpl
│   ├── configmap.yaml
│   ├── deployment.yaml
│   ├── pvc.yaml
│   ├── secrets.yaml
│   └── svc.yaml
└── values.yaml
```

- The Chart.yaml file contains some metadata about the Chart, like its name, version, keywords, and so on, in this case, for MariaDB.
- The values.yaml file contains keys and values that are used to generate the release in your cluster. These values are replaced in the resource manifests using the Go templating syntax.
- The templates directory contains the resource manifests that make up this MariaDB application.

## commands

```bash
# search artifact hub
helm search hub database

# add repo
helm repo add ealenn https://ealenn.github.io/charts
helm repo update

# install tester tool
helm upgrade -i tester ealenn/echo-server --debug

# view chart history
helm list

# uninstall
helm uninstall tester

# download 
helm repo add bitnami https://charts.bitnami.com/bitnami
helm fetch bitnami/apache --untar

# install using downloaded file
helm install anotherweb .
```

helm cache dir: $HOME/.cache/helm/  
