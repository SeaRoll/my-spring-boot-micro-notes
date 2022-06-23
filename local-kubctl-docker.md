# How to pull images from a local docker registry (docker application in your computer)
Apparently, a private docker reigstry is HTTP and not HTTPS. This means that a command line is required in the
kubernetes cluster to locally pull from docker images instead of using something like docker-hub.
```bash
kubectl create secret generic regcred \
  --from-file=.dockerconfigjson=<path/to/.docker>/config.json \
  --type=kubernetes.io/dockerconfigjson
```
This will allow the kubernetes cluster to pull images locally instead of from docker hub
