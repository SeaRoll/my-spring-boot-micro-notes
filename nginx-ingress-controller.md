# Kubernetes Ingress with Nginx
[Kubernetes nginx ingress](https://kubernetes.github.io/ingress-nginx/deploy/#quick-start)

[Issues if ingress is pending in svc](https://github.com/docker/for-mac/issues/4903)

Commands to know:
```sh
kubectl get svc -A
kubectl get deploy -A
kubectl describe ingress
kubectl apply -f <filename>.yaml
```

#### 1. Installing ingress-nginx
Go to vendor folder and then apply the yaml file inside
```
kubectl apply -f ingress-deploy.yaml
```

#### 2. Check that the ingress is running 
```
kubectl get svc -A
```
Note: if the external-ip for the loadbalander is pending, 
restart docker-desktop and then try

#### 3. Apply ingress-service
Configure ingress-service as you want it
```
kubectl apply -f ingress-service.yaml
```

#### Troubleshooting:
Q: My API gets accessed, but the api returns 404.

A: This is because (especially spring-boot) ignores the prefix in 
the ingress-service. apply correct prefix that the controller expects

--
