## 1. 选择 Kubernetes 集群
如果没有现成的 Kubernetes 集群，可以选择网上免费的 Kubernetes 集群资源：

### 1.1 在 kata 中利用 Ubuntu 安装指定版本的 Kubernetes 集群
具体方式可以见：[ubuntu-Kubernetes](https://github.com/yu3peng/ubuntu-Kubernetes)

### 1.2 在 kata 中直接使用 Kubernetes Playgroud
登录 [Kubernetes Playgroud](https://katacoda.com/courses/kubernetes/playground) 使用，本实践采用此种方式进行。


## 2. 安装 Helm 3
```
cd /opt && wget https://get.helm.sh/helm-v3.1.0-linux-amd64.tar.gz
tar -xvf helm-v3.1.0-linux-amd64.tar.gz
mv linux-amd64/helm /usr/local/bin/
```

## 3. 安装 spark-operator
```
helm repo add incubator http://storage.googleapis.com/kubernetes-charts-incubator
kubectl create namespace spark-operator
helm install incubator/sparkoperator --namespace spark-operator --name-template spark
kubectl create serviceaccount spark 
kubectl create clusterrolebinding spark-role --clusterrole=edit --serviceaccount=default:spark --namespace=default
```

## 4. 部署例子
```
kubectl apply -f https://raw.githubusercontent.com/yu3peng/spark-on-k8s-operator/master/examples/spark-py-pi.yaml
```
