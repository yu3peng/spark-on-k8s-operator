## 1. 在 Ubuntu上安装 Kubernetes 集群
具体方式可以见：[ubuntu-Kubernetes](https://github.com/yu3peng/ubuntu-Kubernetes)

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
