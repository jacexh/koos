# 安装过程

## Cluster

```bash
kind create cluster --config kind-config.yml
```

## Kubectl

```bash
sudo curl -fsSLo /etc/apt/keyrings/kubernetes-archive-keyring.gpg https://packages.cloud.google.com/apt/doc/apt-key.gpg
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

### Helm

```bash
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

## Caddy Ingress

<https://github.com/caddyserver/ingress>

**修改Caddy为NodePort，并暴露30000 30001两个端口**

```bash
kubectl create namespace caddy-system
helm install \
  --namespace=caddy-system \
  --repo https://caddyserver.github.io/ingress/ \
  --atomic \
  --set ingressController.config.email=jace.xh@gmail.com \
  mycaddy \
  caddy-ingress-controller
```
