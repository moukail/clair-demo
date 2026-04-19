Podman
======
```bash
podman compose up -d --build
```

Kubernetes
==========
```bash
### Install Minikube
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

minikube config set rootless true
minikube delete
minikube start --driver=podman --container-runtime=cri-o

### Install Kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

### Deploy Clair
kubectl config current-context
kubectl create secret generic clair-config --from-file=clair-config.yaml=./config/clair-config.yaml
kubectl apply -f kubernetes/deployment.yml
```

Clair
=====
```bash
curl -L https://github.com/quay/clair/releases/download/v4.9.0/clairctl-linux-386 -o clairctl
chmod +x clairctl
sudo mv clairctl /usr/local/bin/

minikube service clair-service --url

clairctl report docker.io/library/nginx:1.29.5-alpine3.23
clairctl report --host http://$(minikube ip):30606/ docker.io/library/nginx:1.29.5-alpine3.23
```

[What is Clair?](https://www.redhat.com/en/topics/containers/what-is-clair)
[Clair Documentation](https://quay.github.io/clair/)