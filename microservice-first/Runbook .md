## RUNBOOK

firewall-cmd --add-port=30004/tcp --zone=public --permanent
firewall-cmd --add-port=30005/tcp --zone=public --permanent
firewall-cmd --reload


```
kubectl create -f redis-deploy.yml 
kubectl create -f redis-service.yml 

kubectl create -f postgres-deploy.yml 
kubectl create -f postgres-service.yml 

kubectl create -f voting-app-deploy.yml 
kubectl create -f voting-app-service.yml

kubectl create -f result-app-deploy.yml 
kubectl create -f result-app-service.yml

kubectl create -f worker-app-deploy.yml 
```

```
minikube service voting-service --url
http://192.168.11.31:30004

minikube service result-service --url
http://192.168.11.31:30005
```


```
[root@control-plane ~]# kubectl get all
NAME                                     READY   STATUS    RESTARTS   AGE
pod/postgres-deploy-6f787b796b-jk4pq     1/1     Running   0          4m26s
pod/redis-deploy-5d7988b4bb-95fc7        1/1     Running   0          5m10s
pod/result-app-deploy-6cb79db456-79tmv   1/1     Running   0          72s
pod/voting-app-deploy-74fb89676f-w2q4t   1/1     Running   0          3m24s
pod/worker-app-deploy-799b5fb489-59qjc   1/1     Running   0          31s

NAME                     TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
service/db               ClusterIP   10.101.67.40     <none>        5432/TCP       4m19s
service/kubernetes       ClusterIP   10.96.0.1        <none>        443/TCP        69m
service/redis            ClusterIP   10.106.113.32    <none>        6379/TCP       4m49s
service/result-service   NodePort    10.100.172.173   <none>        80:30005/TCP   63s
service/voting-service   NodePort    10.105.241.167   <none>        80:30004/TCP   2m37s

NAME                                READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/postgres-deploy     1/1     1            1           4m26s
deployment.apps/redis-deploy        1/1     1            1           5m10s
deployment.apps/result-app-deploy   1/1     1            1           72s
deployment.apps/voting-app-deploy   1/1     1            1           3m24s
deployment.apps/worker-app-deploy   1/1     1            1           31s

NAME                                           DESIRED   CURRENT   READY   AGE
replicaset.apps/postgres-deploy-6f787b796b     1         1         1       4m26s
replicaset.apps/redis-deploy-5d7988b4bb        1         1         1       5m10s
replicaset.apps/result-app-deploy-6cb79db456   1         1         1       72s
replicaset.apps/voting-app-deploy-74fb89676f   1         1         1       3m24s
replicaset.apps/worker-app-deploy-799b5fb489   1         1         1       31s
```


