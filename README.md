# kubernetes
kubernetes dashboard项目官方：https://github.com/kubernetes/dashboard/releases

##1、yaml文件:  
 *1.1. kubernetes-dashboard.yaml*  
 *1.2. kubernetes-dashboard-admin.rbac.yaml*  
 *1.3. heapster.yaml*  
 *1.4. heapster-rbac.yaml*  
  注：官方文件中只包含了kubernetes-dashboard.yaml，且kubernetes在1.6版本以后启用了RBAC访问控制策略，直接使用官方版会出现访问权限不足的报错；
    此问题可使用kubectl或Kubernetes API进行配置。使用RBAC可以直接授权给用户，让用户拥有授权管理的权限，这样就不再需要直接触碰Master Node。

相关修改为：
kubernetes-dashboard.yaml 中修改 serviceAccountName，外部访问dashboard的方式（本文为token访问）
kubernetes-dashboard-admin（默认为kubernetes-dashboard）



[root@k8s-master ~]# kubectl apply -n kube-system -f .      # 执行安装  
clusterrolebinding.rbac.authorization.k8s.io/heapster created  
serviceaccount/heapster created  
deployment.extensions/heapster created  
service/heapster created  
serviceaccount/kubernetes-dashboard-admin created  
clusterrolebinding.rbac.authorization.k8s.io/kubernetes-dashboard-admin created  
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply  
secret/kubernetes-dashboard-certs configured  
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply  
serviceaccount/kubernetes-dashboard configured  
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply  
role.rbac.authorization.k8s.io/kubernetes-dashboard-minimal configured  
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply  
rolebinding.rbac.authorization.k8s.io/kubernetes-dashboard-minimal configured  
Warning: kubectl apply should be used on resource created by either kubectl create --save-config or kubectl apply  
deployment.apps/kubernetes-dashboard configured  
service/kubernetes-dashboard-external created  
[root@k8s-master ~]# kubectl get pod -n kube-system |grep kubernetes-dashboard     # 执行完成后查看pod是否正常运行  
kubernetes-dashboard-7897c6748f-l4n7z   1/1     Running   0          2m4s  
kubernetes-dashboard-7d75c474bb-wvfc7   1/1     Running   0          92m  
[root@k8s-master ~]# kubectl get service  -n kube-system |grep kubernetes-dashboard     # 查看服务暴露的端口号  
kubernetes-dashboard            ClusterIP   10.110.109.159   <none>        443/TCP                  93m  
kubernetes-dashboard-external   NodePort    10.108.194.91    <none>        9090:31666/TCP           2m27s  
[root@k8s-master ~]#   


Running状态说明运行正常，直接可通过masterip:端口号访问ui界面。  
可根据需要修改nodePort参数来修改访问端口。  
