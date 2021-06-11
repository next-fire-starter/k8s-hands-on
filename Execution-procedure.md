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
kubectl get pod
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
kubectl get pod
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
お片付け
```
kubectl apply -f replicaset-definition.yml
kubectl get pod
kubectl create -f pod-definition.yml
kubectl get pod
kubectl delete replicaset myapp-replicaset
```
---
### デプロイメント
デプロイメント起動  
デプロイメント確認  
情報確認 ポッド、レプリカセット、デプロイメント、サービス  
お片付け  
```
kubectl apply -f deployment-definition.yml
kubectl get deployment
kubectl get all
kubectl delete deployment myapp-deployment

```
---
### ロールアウト

ロールアウト確認  recodeオプションを付けて履歴に変更内容を追記するように設定  
```
kubectl apply -f deployment-definition.yml --record
kubectl rollout status deployment myapp-deployment
```
イメージを変更して履歴が作成されることを確認  
詳細のイベントでローリングアップデートが実行されている履歴が確認できるrecodeオプションの内容も記載されている  
レプリカセットが新しく作成されていることを確認  
```
kubectl rollout history deployment myapp-deployment
kubectl set image deployment/myapp-deployment nginx-container=nginx:1.9.1 --record
kubectl rollout history deployment myapp-deployment
kubectl describe deployment myapp-deployment
```
ロールアウトアンドゥで更新前へロールバックする  
お片付け  
```
kubectl get replicaset
kubectl rollout undo deployment myapp-deployment
kubectl get replicaset
kubectl delete deployment myapp-deployment
```
---
### サービス  
デプロイメント起動  
サービスを起動    
サービス確認   
お片付け
```
kubectl apply -f deployment-definition.yml
kubectl apply -f service-definition.yml
kubectl get service
minikube service myapp-service --url
http://192.168.11.31:30004

kubectl delete service myapp-service
kubectl delete deployment myapp-deployment
```






