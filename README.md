# trendyol-task1-k8s

Note: The * symbol indicates “Nice to Have” items.
All steps are expected as IaC (able to be reinstalled easily on another machine.)
Setups, tools and processes should be documented. All works should be archived on Git.

### 1. k8s
#### 1.1- Kubernetes Setup
Two servers will be used for the setup;
1 Master, Node role. (Server 0)
1 Node (Server 1)
The base-setup must meet the following requirements.
cluster name: case-<name-surname>.abc
network plugin: flannel
dns mode: coredns
  
#### 1.2- Setup an internal Prometheus server after installation to collect metrics from the cluster, and ensure it only covers a single node.
#### 1.3 Make sure there are no other deployments on the Prometheus node.
#### 1.4- Setup Ingress Controller DaemonSet and enable access to the deployed Prometheus server via the http 80 port.
### 2.	Setup a Server-mode Consul on Server 2 via given servers.
Consul cluster should be setup as a single node.
### 3.	Setup Federation Prometheus on Server 2.
#### 3.1	Use consul-prometheus discovery on prometheus.yaml during Federation
This requires service information from internal Prometheus to be added to service registry of Consul.
### 4.	Setup Grafana on Server 2 or in Kubernetes, and add external Prometheus data source.
#### 4.1	Prepare a dashboard for the installed Kubernetes cluster, with the following memory metrics.
 
Metrics;
Cluster total CPU capacity
Cluster total allocatable CPU
Cluster total requested CPU
Cluster total CPU usage
### 5.	Setup Alertmanager on Server 2, and create a pod_restart alarm for the application deployed in 1.2.
### 6.	Setup Elasticsearch and Kibana on Server 3 and ensure that stdout logs from Kubernetes pods are directed here.
### 7.	Setup a Gitlab on Server 3 and make sure that items 3 and 5 can be triggered over the pipeline.
### 8. Develop a Tool.
#### 8.1	(Tool) A tool must be developed that will generate a dynamic template file (nginx site conf) by importing services from multiple k8s clusters. Services required should be selectable via annotations that will be added to the Kubernetes service object. (e.g. hayde.trendyol.io/enabled: "true")
#### 8.2	Setup and deploy nginx on one of the servers.
#### 8.3	Sent nginx logs to Elasticsearch.
#### 8.4*  Reflect changes to K8s services instantaneously.

