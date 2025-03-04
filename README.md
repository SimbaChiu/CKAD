# CKAD
Repository for Certified Kubernetes Application Developer (CKAD)

# OCI commands (Docker, Podman, Buildah)
Build images from Dockerfiles, name and tag images, save images as tar files.

List current local images
```
docker image ls
podman image ls
buildah images
```

Build images from Dockerfiles
```
docker image build -t <repo>:<tag> .
docker image build -t <repo>:<tag> -f <path>/Dockerfile
podman image build -t <repo>:<tag> .
podman image build -t <repo>:<tag> -f <path>/Dockerfile
buildah build -t <repo>:<tag>
```

Name and tag images
```
docker tag <repo>:<tag> <repo>:<tag>
podman image tag <repo>:<tag> <repo>:<tag>
buildah tag <repo>:<tag> <repo>:<tag>
```

Save images as OCI archives
```
docker save <repo>:<tag> -o <name>.tar
docker save <repo>:<tag> | gzip > <name>.tar.gz
podman save <registry>/<repo>:<tag> -o <name>.tar
```

Create image from a running container
```
docker commit <container> <repo>:<tag>
```

Pull images from (public) repositories
```
docker image pull <repo>:<tag>
```

Delete local images
```
docker image rm <repo>:<tag> -f
docker image rm <image_id> -f
podman image rm <repo>:<tag> -f
podman image rm <image_id> -f
buildah rmi <repo>:<tag> -f
buildah rmi <image_id> -f
```

# Kubectl commands

Set kubectl alias
```
alias k="kubectl"
```

Set namespace
```
kubectl config set-context --current --namespace=<namespace>
```

Modify resources imperatively and declaratively
```
kubectl create deploy [deployment-name] --image=[image-name]:[tag] --dry-run=client -o yaml > deploy.yaml
kubectl create -f ./[folder-name]
kubectl set selector svc [service-name] 'key=value'
kubectl scale deploy [deployment=name] --replicas=1
kubectl set image deploy [deployment-name] [image-name]
KUBE_EDITOR="nano" kubectl edit deploy [deployment-name]
```

Modify deployment with annotations
```
kubectl create if file.deployment.yaml --save-config
kubectl apply -f file.deployment.yaml --record=true
kubectl annotate deployment [name] kubernetes.io/change-cause="Change details" --overwrite=true
```

Rollout status, history, rollback
```
kubectl rollout status deployment [deployment-name]
kubectl rollout history deployment [deployment-name] --revision=2
kubectl rollout undo -f file.deployment.yaml --to-revision=2
```

Get specific property value from a deployment
```
kubectl get deploy web-app -o json | jq '.metadata.annotations."kubernetes.io/change-cause"'
```

# Helm commands

Find charts and repositories
```
helm search hub
helm repo add
helm search repo
```

Learn about chart values
```
helm show values
helm pull --untar
```

Installm update, uninstall a chart
```
helm install
helm upgrade
helm uninstall
```

```
helm install nginx-app bitname/nginx --version=13.1.5 -n dev --set replicaCount=5
```
