#Test environment setup
- Linux server
  - hess@192.168.1.107
  - minikube install : version: v1.26.0
  - kubectl install : Client Version: v1.24.0  Kustomize Version: v4.5.4  Server Version: v1.24.1
- My Windows OS PC
  - Install Docker Engine v20.10.17
- https://hub.docker.com
  - account : hesslee
  - repository : sharding
- https://github.com
  - account : hessalti
  - repository : kube-sharding

#Build docker image
```
docker-working-directory> set DOCKER_BUILDKIT=0
docker-working-directory> docker build --tag hesslee/sharding https://github.com/hessalti/kube-sharding.git#main:docker
```

#Check built image
```
docker-working-directory> docker run -it hesslee/sharding   "/bin/bash"
Windows-cmd> docker push hesslee/sharding
```

#K8s setup
```
linux> minikube start --nodes 2 -p multinode-demo
linux> kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/sharding-svc.yaml
linux> kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/sharding-sc.yaml
linux> kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/sharding-cm.yaml
linux> kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/sharding-sts.yaml
```

#Check sharding pods
```
kubectl exec -it sharding-0 -- /bin/bash
kubectl exec -it sharding-1 -- /bin/bash
```

#Problems
```
volumn root mount
```

#ETC
```
altibase> server create utf8 utf8
## 환경에 따라 필요한 경우가 있는것들... 
root> apt-get update
root > apt-get install vim
root> apt-get install libncurses5-dev  ## for isql
## libncurses 와 libtinfo 를 찾아서 아래 작업을 해준다.
root> ln -s libncurses.so.6.2 libncurses.so.5
root> ln -s libtinfo.so.6.2 libtinfo.so.5
```
