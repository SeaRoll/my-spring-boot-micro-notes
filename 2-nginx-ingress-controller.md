# Kubernetes Ingress with Nginx

[Kubernetes nginx ingress](https://kubernetes.github.io/ingress-nginx/deploy/)

[Issues if ingress is pending in svc](https://github.com/docker/for-mac/issues/4903)

Commands to know:

```sh
kubectl get svc -A
kubectl get deploy -A
kubectl describe ingress
kubectl apply -f <filename>.yaml
```

#### 1. Install helm

[Link](https://helm.sh/docs/intro/install/) is the best on how to install.
If you are using mac, homebrew is recommended with the command:

```sh
brew install helm
```

On linux:

```sh
curl https://baltocdn.com/helm/signing.asc | gpg --dearmor | sudo tee /usr/share/keyrings/helm.gpg > /dev/null
sudo apt-get install apt-transport-https --yes
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/helm.gpg] https://baltocdn.com/helm/stable/debian/ all main" | sudo tee /etc/apt/sources.list.d/helm-stable-debian.list
sudo apt-get update
sudo apt-get install helm
```

#### 2. Installing ingress-nginx

Use helm to install ingress into the kubectl

```sh
helm upgrade --install ingress-nginx ingress-nginx \
  --repo https://kubernetes.github.io/ingress-nginx \
  --namespace ingress-nginx --create-namespace
```

#### 3. Apply ingress-service

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example
  namespace: default
spec:
  ingressClassName: nginx
  rules:
    - host:
      http:
        paths:
          - pathType: Prefix
            backend:
              service:
                name: fraud
                port:
                  number: 80
            path: /api/v1/fraud-check
```

Configure ingress-service as you want it and then:

```
kubectl apply -f ingress-service.yaml
```

#### Troubleshooting:

Q: My API gets accessed, but the api returns 404.

A: This is because (especially spring-boot) ignores the prefix in
the ingress-service. apply correct prefix that the controller expects

--
