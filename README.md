# kind-airflow-grpc-api

### Objective

0. Create Kind Cluster with Storage with Pointing to the local registry
1. Run airflow on Kind cluster with volume.
2. Enable Airflow REST APIs.
3. Deploy simple GRPC Service to the cluster.
4. Build an image
5. Tag an Image
6. Docker push
7. Helm create 
8. Modify Helm - Deploy helm 
9. Trigger DAG from GRPC. (Test)
10. DAG Generator with own Interpretor or Language. 


#### Create cluster
Note: Stop runnning local registry if it is in running mode.

```
./create-cluster.sh
```
Reference:
https://www.astronomer.io/events/recaps/official-airflow-helm-chart/

```
kubectl create namespace airflow
```

Optional steps if you have not 
```
helm repo add apache-airflow https://airflow.apache.org
helm repo update
```

Install Airflow 
```
helm install airflow apache-airflow/airflow --namespace airflow --debug --timeout 10m0s
helm ls -n airflow

```

Change Executor Type to K8s
```
kubectl apply -f variables.yaml
<!-- helm upgrade --install airflow apache-airflow/airflow -n airflow -f values.yaml --debug -->
 kubectl create -f pv.yaml
  kubectl create -f pvc.yaml
  helm upgrade --install airflow apache-airflow/airflow -n airflow -f values.yaml --debug
```