# How to pull images from a local docker registry (docker application in your computer)
Apparently, a private docker reigstry is HTTP and not HTTPS. This means that a command line is required in the
kubernetes cluster to locally pull from docker images instead of using something like docker-hub.

```bash
kubectl create secret generic regcred \
  --from-file=.dockerconfigjson=<path/to/.docker>/config.json \
  --type=kubernetes.io/dockerconfigjson
```

And then to pull images from secrets, you use the example below

```yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: fraud
  labels:
    app: fraud
spec:
  replicas: 1
  template:
    metadata:
      name: fraud
      labels:
        app: fraud
    spec:
      containers:
        - name: fraud
          image: fraud-service
          imagePullPolicy: Never
          ports:
            - containerPort: 8081
          env:
            - name: SPRING_PROFILES_ACTIVE
              value: default
      imagePullSecrets:
        - name: regcred
      restartPolicy: Always
  selector:
    matchLabels:
      app: fraud
---
apiVersion: v1
kind: Service
metadata:
  name: fraud
spec:
  selector:
    app: fraud
  ports:
    - port: 80
      targetPort: 8081
  type: NodePort
```
**note that the imagePullSecrets line is the one that takes the name `regcred` to pull**
**also note that imagePullPolicy should always be Never because if not, it will try to pull from some external sources**
