### Let us install Prometheus & Grafana to Monitor our local kubernetes cluster (Minikube)
#### Chart References : prometheus-community https://prometheus-community.github.io/helm-charts 
#### grafana https://grafana.github.io/helm-charts

Let us add prometheus repo, pull down Prometheus Chart & Check its contents

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm search repo prometheus
helm pull prometheus-community/prometheus

```
Unzip the downloaded tar file and examine its contents

Let us over-ride one value to make the Prometheus Service available on NodePort
First, let us review the modified template using the template command

```
helm template ./prometheus --set server.service.type=NodePort
```
Check if Prometheus Server type has changed to NodePort
If everything looks good, let us go ahead & install Prometheus

```
helm install prometheus ./prometheus --set server.service.type=NodePort
kubectl get po,svc
helm list
helm get manifest prometheus

# Check if you can hit prometheus-server service URL
minikube service prometheus-server

```

Let us now pull down Grafana chart and make similar modifications to expose NodePort Service
```
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update grafana
helm search repo grafana

# Let us pull down grafana/grafana chart
helm pull grafana/grafana
```

Unzip and examine the Manifests
Let us modify the service to get a NodePort

```
helm install grafana ./grafana --dry-run --debug --set service.type=NodePort
# Check manifests and if everything looks good, let us install it
helm install grafana ./grafana --set service.type=NodePort
kubectl get po,svc

# Once all Pods come up, check if grafaba service is accessible
minikube service grafana

```
Connect Prometheus Data Source to Grafana Dashboard to visualise local cluster monitoring!!