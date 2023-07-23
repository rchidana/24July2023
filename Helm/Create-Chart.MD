### Let us create a simple Helm3 chart from Scratch

```
helm create nginx-chart
tree /f /a


\---nginx-chart
    |   .helmignore
    |   Chart.yaml
    |   values.yaml
    |
    +---charts
    \---templates
        |   deployment.yaml
        |   hpa.yaml
        |   ingress.yaml
        |   NOTES.txt
        |   service.yaml
        |   serviceaccount.yaml
        |   _helpers.tpl
        |
        \---tests
                test-connection.yaml

```

+ .helmignore: It is used to define all the files which we don’t want to include in the helm chart. It works similarly to the .gitignore file.
+ Chart.yaml: It contains information about the helm chart like version, name, description, etc
+ values.yaml: In this file, we define the values for the YAML templates. For example, image name, replica count, HPA values, etc. You can override these values dynamically or at the time of installing the chart using --values or --set command
+ charts: We can add another chart’s structure inside this directory if our main charts have some dependency on others. By default this directory is empty
+ templates: This directory contains all the Kubernetes manifest files that form an application. These manifest files can be templated to access values from values.yaml file. Helm creates some default templates for Kubernetes objects like deployment.yaml, service.yaml etc, which we can use directly, modify, or override with our files
+ templates/NOTES.txt: This is a plaintext file that gets printed out after the chart is successfully deployed
+ templates/_helpers.tpl: That file contains several methods, and sub-template. These files are not rendered to Kubernetes object definitions but are available everywhere within other chart templates for use 
+ templates/tests/: We can define tests in our charts to validate that your chart works as expected when it is installed

#### Let us modify chart.yaml with the following contents

```
apiVersion: v2
name: nginx-chart
description: My First Helm Chart
type: application
version: 0.1.0
appVersion: "1.0.0"
maintainers:
- email: anandr72@gmail.com
  name: anand

```

+ apiVersion: This denotes the chart API version. v2 is for Helm 3 and v1 is for previous versions
+ name: Denotes the name of the chart
+ description: Denotes the description of the helm chart
+ Type: The chart type can be either ‘application’ or ‘library’. Application charts are what you deploy on Kubernetes. Library charts are re-usable charts that can be used with other charts. A similar concept of libraries in programming
+ Version: This denotes the chart version
+ appVersion: This denotes the version number of our application (Nginx)
+ maintainers: Information about the owner of the chart

Let us remove all files in the 'templates' folder (since our chart is pretty simple) and let us put up a simple deployment.yaml which will use the following objects for dynamically picking up values:

+ Release: Every helm chart will be deployed with a release name. If you want to use the release name or access release-related dynamic values inside the template, you can use the release object
+ Chart: If you want to use any values you mentioned in the chart.yaml, you can use the chart object
+ Values: All parameters inside values.yaml file can be accessed using the Values object

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: {{ .Release.Name }}-nginx
  labels:
    app: {{ .Release.Name }}
spec:
  replicas: {{ .Values.replicaCount }}
  selector:
    matchLabels:
      app: {{ .Release.Name }}
  template:
    metadata:
      labels:
        app: {{ .Release.Name }}
    spec:
      containers:
        - name: {{ .Chart.Name }}
          image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}"
          imagePullPolicy: {{ .Values.image.pullPolicy }}
          ports:
            - name: http
              containerPort: {{ .Values.service.port }}
              protocol: TCP
          volumeMounts:
            - name: nginx-index-file
              mountPath: /usr/share/nginx/html/
      volumes:
        - name: nginx-index-file
          configMap:
            name: {{ .Release.Name }}-index-html-configmap

```

Helm uses Go Template Engine : https://pkg.go.dev/text/template

+ name: name: {{ .Release.Name }}-nginx
+ container name: {{ .Chart.Name }} - will be picked from chart.yaml
+ Replicas: {{ .Values.replicaCount }} and image: "{{ .Values.image.repository }}:{{ .Values.image.tag }}" - Both will be picked from values.yaml

Create service.yaml to expose our deployment and let us templatise it as well:

```
apiVersion: v1
kind: Service
metadata:
  name: {{ .Release.Name }}-service
spec:
  selector:
    app: {{ .Release.Name }}
  type: {{ .Values.service.type }}
  ports:
    - protocol: {{ .Values.service.protocol | default "TCP" }}
      port: {{ .Values.service.port }}

```

Check the pipe directive : protocol: {{ .Values.service.protocol | default "TCP" }} 

Go Template directives for further reference: 
* Builtin Objects in Helm : https://helm.sh/docs/chart_template_guide/builtin_objects/ 
* Functions & Pipeline : https://helm.sh/docs/chart_template_guide/functions_and_pipelines/ 
* Template function list : https://helm.sh/docs/chart_template_guide/function_list/ 
* Flow Control Structures : https://helm.sh/docs/chart_template_guide/control_structures/ 
* Variables : https://helm.sh/docs/chart_template_guide/variables/ 

To replace the default nginx index.html, let us create a configMap with some HTML content.
Create configmap.yaml with following content:

```
apiVersion: v1
kind: ConfigMap
metadata:
  name: {{ .Release.Name }}-index-html-configmap
  namespace: default
data:
  index.html: |
    <html>
    <h1>Welcome</h1>
    </br>
    <h1>Hi! I got deployed in {{ .Values.env.name }} Environment using Helm Chart </h1>
    </html

```
Check the HTML content which picks up Environment details from {{ .Values.env.name }}

Finally let us create values.yaml with the following contents:

```
replicaCount: 2

image:
  repository: nginx
  tag: "1.16.0"
  pullPolicy: IfNotPresent

service:
  name: nginx-service
  type: ClusterIP
  port: 80

env:
  name: dev

```

We are all done and let us check our chart by linting it:

```
# Depending upon your $pwd
helm lint nginx-chart
# OR 
helm lint .

# Let us also render our template files WITHOUT INSTALLING IT (just to validate)
helm template nginx-chart 

# Let us also do a dry-run
helm install --dry-run nginx-dev nginx-chart

# If Everything looks good, let us go ahead & install the Chart
helm install front-end-dev nginx-chart
helm list
# Check the revision number
kubectl get po,svc,deploy

```

Chart Upgrade & Rollback

Let us make some changes to the chart, say reduce replicaCount to 1 in values.yaml and perform an upgrade

```
helm upgrade front-end-dev nginx-chart
helm list
# Check the revision number & also the replica count
k get po

```

We can also rollback our changes to the previous one or any other revision of our choice by specifying the rollback command : helm rollback <release-name> <revision-number>

```
helm rollback front-end-dev
helm list
k get po
```

Source Code for this chart is available at : https://github.com/rchidana/nginx-chart 
