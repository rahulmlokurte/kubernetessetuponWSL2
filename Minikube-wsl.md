# Minikube with Docker driver

## Install Minikube on WSL2

- curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
- sudo install minikube-linux-amd64 /usr/local/bin/minikube

## Start the docker service on WSL2

- sudo service docker start

## Start minikube cluster using Docker driver

- minikube config set driver docker
- minikube start --driver=docker --container-runtime=containerd --alsologtostderr -v=1

## Dashboard

- minikube dashboard

## Deploy applications

- kubectl create deployment hello-minikube --image=k8s.gcr.io/echoserver:1.4
- kubectl expose deployment hello-minikube --type=NodePort --port=8080
- kubectl get services hello-minikube

## Access the service using:
- minikube service hello-minikube 
- kubectl port-forward service/hello-minikube 7080:8080
- curl http://{minikube-ip}:{nodeport}

## Ingress

- minikube addon ingress
- minikube addon ingress-dns
- minikube addon list
- Add the dns name in */etc/hosts* as below where *192.168.49.2* is minikube ip

```sh
192.168.49.2    hello-world.info
192.168.49.2    hello-john.test
192.168.49.2    hello-jane.test
```

- Add below in */etc/resolvconf/resolv.conf.d/base*

```sh
search test
nameserver 192.168.49.2
nameserver 8.8.8.8
nameserver 8.8.4.4
timeout 5
```

- Add below in */etc/resolvconf/resolv.conf.d/head*

```sh
nameserver 8.8.4.4
nameserver 8.8.8.8
```



