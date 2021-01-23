# airflowplus 

## command set
```
kubectl apply -f airflowplus.yml
kubectl apply -f airflowplus_namespace.yml
```

## expose ports for deployment, redis, postgres
```
kubectl expose deployment airflowplus --type NodePort --port 8080,6379,5432 -n airflowplus
```

## showing deployment
```
kubectl get all -n airflowplus
```
```

NAME                               READY   STATUS    RESTARTS   AGE
pod/airflowplus-6bdf569756-b848w   3/3     Running   0          5m31s

NAME                  TYPE       CLUSTER-IP      EXTERNAL-IP   PORT(S)                                        AGE
service/airflowplus   NodePort   10.107.46.171   <none>        8080:31730/TCP,6379:30555/TCP,5432:31483/TCP   19s

NAME                          READY   UP-TO-DATE   AVAILABLE   AGE
deployment.apps/airflowplus   1/1     1            1           5m31s

NAME                                     DESIRED   CURRENT   READY   AGE
replicaset.apps/airflowplus-6bdf569756   1         1         1       5m31s

```

## showing service/airflowplus
```
kubectl describe service airflowplus -n airflowplus
```
```

Name:                     airflowplus
Namespace:                airflowplus
Labels:                   app=airflowplus
Annotations:              <none>
Selector:                 app=airflowplus
Type:                     NodePort
IP Families:              <none>
IP:                       10.107.46.171
IPs:                      10.107.46.171
Port:                     port-1  8080/TCP
TargetPort:               8080/TCP
NodePort:                 port-1  31730/TCP
Endpoints:                172.17.0.6:8080
Port:                     port-2  6379/TCP
TargetPort:               6379/TCP
NodePort:                 port-2  30555/TCP
Endpoints:                172.17.0.6:6379
Port:                     port-3  5432/TCP
TargetPort:               5432/TCP
NodePort:                 port-3  31483/TCP
Endpoints:                172.17.0.6:5432
Session Affinity:         None
External Traffic Policy:  Cluster
Events:                   <none>

```

## set LOAD_EX=y into deployment
```
kubectl set env deployment airflowplus LOAD_EX=y -n airflowplus
deployment.apps/airflowplus env updated
```

## restart deployment in order to activate new parameter above
```
kubectl scale deployment airflowplus --replicas=0 -n airflowplus
deployment.apps/airflowplus scaled
```
```
kubectl scale deployment airflowplus --replicas=1 -n airflowplus
deployment.apps/airflowplus scaled
```

## output
<>
