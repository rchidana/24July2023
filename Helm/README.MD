### Helm Useful Instructions

### Helm Official reference : https://helm.sh/ 

### Helm Architecture : https://helm.sh/docs/topics/architecture/ 

### Helm Instalaltion Reference : https://helm.sh/docs/intro/install/ 

#### Installing Helm on Ubuntu 22.04

```
curl https://baltocdn.com/helm/signing.asc | sudo apt-key add -
sudo apt-get install apt-transport-https --yes
echo "deb https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm

helm version
```

### Artifact Hub for Public Charts : https://artifacthub.io/packages/search?kind=0 

#### Chart : A Chart is a Helm package & it's a collection of files (mostly YAML) organized in a specific directory structure. It contains all of the resource definitions necessary to run an application, tool, or service inside of a Kubernetes cluster
#### Repository: A Repository is the place where charts can be collected and shared
#### Release: A Release is an instance of a chart running in a Kubernetes cluster. One chart can often be installed many times into the same cluster (with different configurations)

### Helm 101
### Commands to add a Repo, search for specific releases, download & install a Helm Chart

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update

# Search all available charts within prometheus repo
helm search repo prometheus

# Let us install a chart by specifying a name
# --generate name option can be specified to generate a random chart name
helm install --help
helm install prometheus prometheus-community/prometheus

# To override default values in a chart, --values/-f flag or --set flag can be used
helm install -f myvalues.yaml prometheus prometheus-community/prometheus
# OR
helm install --set image=my-image prometheus-community/prometheus

# Check if all the pods have come up without any problems
kubectl get po -A

# Check list of helm charts installed in the cluster(all namespaces)
helm list -A

# helm uninstall can be used to remove a deployed chart
# --keep-history option can be specified in case release history has to me maintained for Audit purposes
helm uninstall prometheus --keep-history

helm status prometheus

# undelete command can be used for performing rollbacks (in this case, it will install prometheus which we just uninstalled)
helm rollback --help
helm rollback prometheus
```

