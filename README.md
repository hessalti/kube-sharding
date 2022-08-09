### Test environment setup
- https://github.com/hessalti/kube-sharding
  - account : hessalti
  - repository : kube-sharding
- https://hub.docker.com/r/hesslee/sharding
  - account : hesslee
  - repository : sharding
- Linux server
  - hess@192.168.1.107
  - minikube install : version: v1.26.0
  - kubectl install : Client Version: v1.24.0  Kustomize Version: v4.5.4  Server Version: v1.24.1
- My Windows OS PC
  - Install Docker Engine v20.10.17

### Prepare altibase_home directory
```
rm -rf altibase_home/dbs
rm -rf altibase_home/logs
rm -rf altibase_home/xlogs
rm -rf altibase_home/arch_logs
rm -rf altibase_home/trc
rm -rf altibase_home/ZookeeperServer.tar.gz
rm -rf altibase_home/ZookeeperServer/apache-zookeeper-3.5.6-bin.tar.gz
```

### Build docker image
```
# prepare Dockerfile & altibase_home in this directory
set DOCKER_BUILDKIT=0
docker build --tag hesslee/sharding .
# Check built image
docker run -it hesslee/sharding   "/bin/bash"
docker push hesslee/sharding
```

### K8s setup
```
# 1 control node, 2 worker nodes
minikube start --nodes 4 -p multinode-demo
kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/base.yaml
kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/zk-cm.yaml
kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/zk-sts.yaml
kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/sd-cm.yaml
kubectl apply -f https://raw.githubusercontent.com/hessalti/kube-sharding/main/kube/sd-sts.yaml
```

### Check sharding pods
```
kubectl get pod -o wide -w
kubectl exec -it sd-1 -- /bin/bash
bash# . ./altibase_home/config_map/set.env     
      ./altibase_home/ZookeeperServer/zkCli.sh -server zk-cs:2181
      ls -R /
bash# is
iSQL> set vertical on;
      select * from sys_shard.LOCAL_META_INFO_;
      node[data] select shard_node_name() POD_NAME, * from sys_shard.LOCAL_META_INFO_;
      select * from X$ZOOKEEPER_DATA_INFO;
      select * from sys_shard.nodes_;
```

### Sharding test
```
iSQL> EXEC DBMS_SHARD.SET_SHARD_TABLE_SHARDKEY('SYS', 'T1', 'P1 SD-0, P2 SD-1, P3 SD-1, P4 SD-1');
      insert into t1 values (1000);
      insert into t1 values (2000);
      insert into t1 values (3000);
      insert into t1 values (4000);
      insert into t1 values (5000);
      commit;
      select shard_node_name() POD_NAME, * from t1;
```

### ETC
```
............
```
