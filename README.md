# How to install One node minikube Kubernetes cluster in WSL 2

The Windows Subsystem for Linux will run the linux environment on Windows. We will install all the required componenets to setup one node minikube kubernetes cluster in WSL2.

## Install WSL

- Install any supported linux distributions on WSL2. Verify the supported linux distribution using the below command.

```sh
    wsl --list --online
```

- Install the required Linux distributions using the below command.

```sh
    wsl --install -d <Distribution Name>
```

## Install Podman

```sh
. /etc/os-release
sudo sh -c "echo 'deb http://download.opensuse.org/repositories/devel:/kubic:/libcontainers:/stable/x${NAME}_${VERSION_ID}/ /' > /etc/apt/sources.list.d/devel:kubic:libcontainers:stable.list"
wget -nv https://download.opensuse.org/repositories/devel:kubic:libcontainers:stable/x${NAME}_${VERSION_ID}/Release.key -O Release.key
sudo apt-key add - < Release.key
sudo apt-get update -qq
sudo apt-get -qq -y install podman
sudo mkdir -p /etc/containers
echo -e "[registries.search]\nregistries = ['docker.io', 'quay.io']" | sudo tee /etc/containers/registries.conf
```

## Install Buildah

```sh
sudo apt-get -y update
sudo apt-get -y install buildah
```

Check out the links to learn more about [Podman](https://podman.io/) and [Buildah](https://buildah.io/)

## Install Minikube

Install minikube and run with podman driver using below command

```sh
minikube start --driver=podman --container-runtime=cri-o --extra-config=kubelet.cgroup-driver=systemd
```

If you are unable to start, you can delete all the cluster using below command and restart the service

```sh
minikube delete --all
```

If you are behind the corporate networks, you need to install the Root Certificate into the minikube cluster using this [link](https://minikube.sigs.k8s.io/docs/handbook/untrusted_certs/)

## Install kubectl

The tool allows you to run commands against Kubernetes clusters. Install Kubectl using this [link](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/).
