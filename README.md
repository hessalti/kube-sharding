## Prepare Altibase sharding package
Copy altibase_home.tgz to docker working directory
 
## Test environment setup
-- My Windows OS PC
-- Install Docker Engine v20.10.17

## Refer Dockerfile : 
docker-working-directory> docker build --tag hesslee/sharding .

# Check built image
Windows-cmd> docker run -it -v C:\Users\ALTIBASE\my-docker:/data  hesslee/sharding   "/bin/bash"
Windows-cmd> docker push hesslee/sharding

## Test environment setup
-- hess@192.168.1.107
-- minikube install : version: v1.26.0
-- kubectl install : Client Version: v1.24.0  Kustomize Version: v4.5.4  Server Version: v1.24.1

minikube start --nodes 2 -p multinode-demo
kubectl apply -f https://raw.githubusercontent.com/hessalti/work/main/kube-sharding/sharding-svc.yaml
kubectl apply -f https://raw.githubusercontent.com/hessalti/work/main/kube-sharding/sharding-sts.yaml
## check sharding pods
kubectl exec -it sharding-0 -- /bin/bash

****** problem : volumn root mount
****** problem : no environment variable setting

altibase> server create utf8 utf8
## 환경에 따라 필요한 경우가 있는것들... 
root> apt-get update
root > apt-get install vim
root> apt-get install libncurses5-dev  ## for isql
## libncurses 와 libtinfo 를 찾아서 아래 작업을 해준다.
root> ln -s libncurses.so.6.2 libncurses.so.5
root> ln -s libtinfo.so.6.2 libtinfo.so.5
