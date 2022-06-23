# Kubernetes Ingress with Nginx
[source](https://matthewpalmer.net/kubernetes-app-developer/articles/kubernetes-ingress-guide-nginx-example.html)

#### Start by creating the “mandatory” resources for Nginx Ingress in your cluster.
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/mandatory.yaml
```

#### If you’re using Docker for Mac to run Kubernetes
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/master/deploy/provider/cloud-generic.yaml
```

#### Check that it’s all set up correctly.
```bash
kubectl get pods --all-namespaces -l app=ingress-nginx
```

#### Create an ingress.yaml and then add this example
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  name: example-ingress
  annotations:
    ingress.kubernetes.io/rewrite-target: /
spec:
  rules:
  - http:
      paths:
        - path: /apple
          backend:
            serviceName: apple-service
            servicePort: 5678
        - path: /banana
          backend:
            serviceName: banana-service
            servicePort: 5678
```

#### Create the Ingress in the cluster
```bash
kubectl create -f ingress.yaml
```
