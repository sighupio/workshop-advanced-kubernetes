# Advanced Kubernetes Workshop by [SIGHUP](https://sighup.io)

Welcome to the Advanced Kubernetes workshop. This workshop is organized by [SIGHUP](https://sighup.io) and aims to provide a comprehensive deep dive on the fundamentals of Kubernetes, on the patterns and best practices that could be adopted while developing distributed applications and microservices architectures on Kubernetes.

If you are interested in this workshop or want an on-site training, you can [email us](mailto:training@sighup.io) for more information.

## Workshop info

This workshop can be delivered in two forms: both as a 2-days and as a 3 days workshop.

### Program

#### Day 1

- Docker quick recap and review (Build, Ship, Run)
- Kubernetes foundations:
  - Nodes
  - Labels & Selectors
  - Pods
  - ReplicaSets & Deployments
  - Deployments in actions: automated Rollouts and Rollbacks
  - Resource Quotas & Limits
- Storage & Configurations:
  - Volumes
  - ConfigMaps & Secrets
- Exposing Services in Kubernetes:
  - Services
  - Service Discovery
  - Ingresses
- Deployment strategies:
  - Canary
  - Blue/Green Deployment
- Other types of objects:
  - DaemonSets
  - Stateulsets & Stateful workloads
  - Jobs & CronJobs

#### Day 2
- Probing
- RBAC & Security Policies
- Patterns for development
- Distributing applications on Kubernetes
  - Kustomize
  - Helm
- An introduction on the Kubernetes architecture

#### Day 3
- Cloud Native monitoring with Prometheus
  - Prometheus monitoring architecture
  - Configuration and Relabeling
  - Alertmanager and Alerting Rules
  - A better way to handle Prometheus: Prometheus Operator
- Centralized Logging with Fluentd + Elasticsearch + Kibana
- Kubernetes Disaster Recovery with Velero
- HA Kubernetes & Cluster Lifecycle Management


## Setup & Environment

You will need to have a laptop (Windows, Linux or Mac), it is preferred for your machine to have at least 8GB of RAM. This isn't strictly required but highly recommended. Working with VMs and Containers **is** resource intensive, no way to get around it.

#### Kubernetes

You should have access to a Kubernetes cluster. You can very easily provision a single-node cluster on your machine with `minikube` as well can use any other Kubernetes cluster from public clouds or self-provisioning.

##### Hypervisor

For this workshop you will need an hypervisor installed on your machine. If you don't have one compatible with Minikube on your machine, you can [install Virtualbox for free](https://www.virtualbox.org/).

##### Minikube
Here you can find [installation instructions](https://github.com/kubernetes/minikube#installation) for your system to easily get `minikube` up and running. Note that you will need to have a hypervisor installed (something like Virtualbox).

For macOS:

```shell
brew cask install minikube
```

For Linux:
```shell
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 \
  && sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

For Windows:
Instructions will depend on the version of the OS. [Refer to the official documentation](https://github.com/kubernetes/minikube#windows), you can find the binary version for manual installation [here](https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe)

#### Kubectl
You will need to install `kubectl`. `Kubectl` is the CLI tool to interact with Kubernetes.

On macOS:
```shell
brew install kubernetes-cli
```

On Linux Ubuntu/Debian:
```shell
sudo apt-get update && sudo apt-get install -y apt-transport-https
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

For other OS, refer to the [official install docs](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl)

As a bonus, you should install `kubectx` and `kubens` [(installation instructions here)](https://github.com/ahmetb/kubectx#installation), they are not strictly required but are actually priceless, so... why not.

#### Kustomize
Kustomize is needed to ease the handling and the customization of multiple
manifest files.

To install
```shell
opsys=linux  # or darwin, or windows
curl -L -O https://github.com/kubernetes-sigs/kustomize/releases/download/v1.0.10/kustomize_1.0.10_${opsys}_amd64
mv kustomize_*_${opsys}_amd64 kustomize
chmod u+x kustomize
```

#### Helm
Helm is a package manager for Kubernetes.

To install Helm, [here you can find the installation instructions](https://github.com/helm/helm#install)

### Using Minikube

Use the following commands to start a minikube cluster and link it to your local installation of docker.

```shell
# Starting a local minikube cluster of 1 node
minikube start --cpus=2 --memory=8192
# Checking nodes
kubectl get pods
# Using docker from minikube
eval $(minikube docker-env)
# Check if linking succeeded
docker ps
```

#### Setting up minikube

Minikube is a simple one-node installation of Kubernetes specifically designed to work on your local machine.

Do the following commands to setup the minikube installation:

2. `minikube ssh` to get into the machine
3. From inside the machine run the following script to download all the Docker images you'll need in the workshop
```
#!/bin/sh
docker pull alpine:3.8
docker pull docker.elastic.co/elasticsearch/elasticsearch:6.4.1
docker pull docker.elastic.co/kibana/kibana:6.4.1
docker pull elasticsearch:5.4.3
docker pull gcr.io/google_containers/fluentd-elasticsearch:1.22
docker pull grafana/grafana:5.3.4
docker pull justwatch/elasticsearch_exporter:1.0.2
docker pull kibana:5.4.3
docker pull mongo:4.1.5-xenial
docker pull nginx:1.7.9
docker pull nginx:1.9.1
docker pull nginx:alpine
docker pull perl
docker pull progrium/stress:latest
docker pull quay.io/prometheus/alertmanager:v0.15.3
docker pull quay.io/prometheus/node-exporter:v0.17.0
docker pull quay.io/prometheus/prometheus:v2.4.3
docker pull quay.io/sighup/mongodb_exporter:v0.6.2
docker pull redis
docker pull sighup/fluentd-elasticsearch:1.2.8
docker pull sighup/powerapp-backend
docker pull sighup/powerapp-frontend
```
4. Stop minikube without destroying it with `minikube stop`

If you don't know what those commands are for or how they work specifically, do not worry. We will review them during the workshop.
