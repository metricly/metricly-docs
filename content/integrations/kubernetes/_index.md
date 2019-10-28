---
title: "Kubernetes"
#date: 2018-12-11
draft: false
tags: ["#kubernetes", "#integrations" ]
author: Lawrence Lane
---
This integration allows you to monitor the data and elements from your Kubernetes environments. Setup is quick, with data appearing in your account as soon as 5 minutes after installation.

## Prerequisites
These steps assume you have already spun up a Kubernetes cluster and can interact with it using the `kubectl` command. If you have not yet set up Kubernetes, see their [GitHub documentation](https://github.com/kubernetes/kubernetes).

### Using RBAC?

If you are implementing Kubernetes with **Role-based Access Control** ([RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)), you must include [ClusterRoleBinding instructions](https://raw.githubusercontent.com/metricly/heapster/master/deploy/kube-config/rbac/heapster-rbac.yaml) to the Metricly deployment YAML file found in step 1.1. These instructions allow metrics to be collected. Simply add the following to your [YAML file](https://raw.githubusercontent.com/metricly/heapster/master/deploy/kube-config/metricly/heapster.yaml) and complete the setup instructions as written.

```
kind: ClusterRoleBinding
apiVersion: rbac.authorization.k8s.io/v1beta1
metadata:
  name: heapster
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: system:heapster
subjects:
- kind: ServiceAccount
  name: heapster
  namespace: kube-system
```

## 1. Download Heapster YAML File
1. [Download this file](https://raw.githubusercontent.com/metricly/heapster/master/deploy/kube-config/metricly/heapster.yaml).
2. Open terminal and locate your YAML file.
3. Name the file `config.yaml`.
4. Replace the `{apiKey}` value in the YAML file with the one found in Metricly under **Integrations** > **Kubernetes**.
![kube api key](/images/_index/kube-api-key.png)

```
apiVersion: v1
kind: ServiceAccount
metadata:
  name: heapster
  namespace: kube-system
---
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: heapster
  namespace: kube-system
spec:
  replicas: 1
  template:
    metadata:
      labels:
        task: monitoring
        k8s-app: heapster
    spec:
      serviceAccountName: heapster
      containers:
      - name: heapster
        image: index.docker.io/metricly/heapster:0.0.5
        imagePullPolicy: IfNotPresent
        command:
        - /heapster
        - --source=kubernetes:https://kubernetes.default
        - --sink=metricly:https://api.us.cloudwisdom.virtana.com/ingest/kubernetes?apiKey={apiKey}
---
apiVersion: v1
kind: Service
metadata:
  labels:
    task: monitoring
    # For use as a Cluster add-on (https://github.com/kubernetes/kubernetes/tree/master/cluster/addons)
    # If you are using this as an addon, you should uncomment this line.
    # kubernetes.io/cluster-service: 'true'
    # kubernetes.io/name: Heapster
  name: heapster
  namespace: kube-system
spec:
  ports:
  - port: 80
    targetPort: 8082
  selector:
    k8s-app: heapster
```
5\. **Save** and close the file.

## 2. Run Setup Command
1. Run the following command in terminal. Make sure that you use the correct path to your config file.

```
kubectl create -f path/to/heapster/config.yaml
```
2\. Verify that your **heapster pod** is running with the below command. It should state `READY 1/1` and `STATUS Running` next to a heapster pod.

```
kubectl get pods --namespace-kube-system
```

3\. View Your Data
Once setup is complete, it takes approximately 5 minutes for data to display in Metricly. All metrics can be found on the [metrics page][1], and your Kubernetes elements can be found in the [inventory page][2].

If you do not wish to use the packaged policies and dashboards that Metricly provides, navigate to **Integrations** > **Kubernetes** and disable the `PACKAGES` toggle.

[1]: /data-visualizaiton/metrics
[2]: /capacity-monitoring/inventory

## Kubernetes Types

Once you have installed this package, the Inventory tab updates to include the following filterable element types:

- Cluster
- Namespace
- Node
- Pod
- Pod Container
- Sys Container
