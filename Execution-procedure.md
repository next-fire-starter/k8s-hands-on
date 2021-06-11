## 実行手順

---
### ポッド
ポッド起動  
ポッド確認  
お片付け  
```
kubectl apply -f pod-definition.yml
kubectl get pods
kubectl delete pod myapp-pod
```
---
### レプリケーションコントローラ
レプリケーションコントローラ起動  
レプリケーションコントローラ確認  
ポッド確認(POD名はコントローラ名の後ろに任意の名前が設定される)  
お片付け  
```
kubectl apply -f rc-definition.yml
kubectl get replicationcontroller
kubectl get pods
kubectl delete replicationcontroller myapp-rc
```
１つ削除しても３つを維持しようとして別なPODを起動することを確認

---
### レプリカセット
レプリカセット起動  
レプリカセット確認
ポッド確認  
レプリカセット削除  
```
kubectl apply -f replicaset-definition.yml
kubectl get replicaset myapp-replicaset
kubectl get pods
kubectl delete replicaset myapp-replicaset
```
１つ削除しても３つを維持しようとして別なPODを起動することを確認

PODを６へ変更する方法１ kubectl replace
replicaset-definition.ymlの  replicas: 3→6へ変更して
```
kubectl replace -f replicaset-definition.yml
```

PODを６へ変更する方法2 kubectl scale マニフェストファイルは変更されない  
２つの書き方ができる、１つはマニフェスト指定、もう一つは起動中のreplicaset名前指定  
```
kubectl scale --replicas=6 -f replicaset-definition.yml
kubectl scale --replicas=6 replicaset myapp-replicaset
```
PODを６へ変更する方法3 kubectl edit マニフェストファイルは変更されない  
```
kubectl edit replicaset myapp-replicaset
```

同じ名前のPODを１つ増やしてもreplicasetで指定した数より多く起動しない  
```
kubectl apply -f replicaset-definition.yml
kubectl get pods
kubectl create -f pod-definition.yml
kubectl get pods
kubectl delete replicaset myapp-replicaset
```
---
### デプロイメント
デプロイメント起動
デプロイメント確認
情報確認 ポッド、レプリカセット、デプロイメント、ノード
```
kubectl apply -f pod-definition.yml
kubectl get deployment
kubectl get all
kubectl delete deployment myapp-deployment

```
