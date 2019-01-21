# Kubernetes Application Design Workshop by [SIGHUP](https://sighup.io)

Welcome to the Kubernetes Application Design and Delivery workshop. This workshop is organized by [SIGHUP](https://sighup.io) and aims to provide a comprehensive deep dive on the fundamentals of Kubernetes, on the patterns and best practices that could be adopted while developing distributed applications and microservices architectures on Kubernetes.

## Workshop info

The first community edition of this workshop has been develivered at [Codemotion Milan 2018](https://milan2018.codemotionworld.com/workshop/kubernetes-application-design-and-delivery/).

In this repo you will find all the code used during the workshop. If you are interested in this workshop or want an on-site training, you can [email us](mailto:training@sighup.io) for more information.

### Setup & Environment

You will need to have a laptop (Windows, Linux or Mac), it is preferred for your machine to have at least 8GB of RAM. This isn't strictly required but highly recommended. Working with VMs and Containers **is** resource intensive, no way to get around it.

#### Kubernetes

You should have access to a Kubernetes cluster. You can very easily provision a single-node cluster on your machine with `minikube` as well can use any other Kubernetes cluster from public clouds or self-provisioning.

##### Hypervisor

For this workshop you will need an hypervisor installed on your machine. If you don't have one compatible with Minikube on your machine, you can [install Virtulbox for free](https://www.virtualbox.org/).

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
Instructions will depend on the version of the OS. [Refer to the official documentaion](https://github.com/kubernetes/minikube#windows), you can find the binary version for manual installation [here](https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe)

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

#### Helm and Kustomize

Install `kustomize` and `helm`. To install Kustomize, [here you can find the installation instructions](https://github.com/kubernetes-sigs/kustomize/blob/master/docs/INSTALL.md). Same goes for [helm](https://github.com/helm/helm#install)

### Using Minikube

Use the following commands to start a minikube cluster and link it to your local installation of docker.

```shell
# Starting a local minikube cluster of 1 node
minikube start --cpus=2 --memory=4096 --kubernetes-version=v1.11.4
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
3. From inside the machine do `docker pull sighup/powerapp-frontend`, `docker pull sighup/powerapp-backend`, `docker pull docker pull mongo:4.1.5-xenial`
4. Stop minikube without destroying it with `minikube stop`

If you don't know what those commands are for or how they work specifically, do not worry. We will review them during the workshop.
