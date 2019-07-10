# kubernetes
kubernetes dashboard项目官方：https://github.com/kubernetes/dashboard/releases

*kubernetes-dashboard.yaml     
*kubernetes-dashboard-admin.rbac.yaml
*heapster.yaml
*heapster-rbac.yaml
注：官方文件中只包含了kubernetes-dashboard.yaml，且kubernetes在1.6版本以后启用了RBAC访问控制策略，直接使用官方版会出现访问权限不足的报错；
    此问题可使用kubectl或Kubernetes API进行配置。使用RBAC可以直接授权给用户，让用户拥有授权管理的权限，这样就不再需要直接触碰Master Node。

相关修改为：
kubernetes-dashboard.yaml 中修改 serviceAccountName，外部访问dashboard的方式（本文为token访问）
kubernetes-dashboard-admin（默认为kubernetes-dashboard）


