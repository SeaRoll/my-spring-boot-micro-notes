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
apiVerstion: v1
kind: Pod
metadata:
  name: private-reg
spec:
  containers
  - name: private-reg-container
    image: <your-private-image>
  imagePullSecrets:
  - name: regcred
```
**note that the imagePullSecrets line is the one that takes the name `regcred` to pull from
