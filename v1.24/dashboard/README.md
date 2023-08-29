1. dashboard-v2.7.0.yaml适用于1.24版本的kubernetes。这个文件里面，deployment增加了http 8080端口。在svc中，配置了80:8080的对应关系.
2. 生产环境中，用的是istio gateway功能。在kubernetes-dashboard名称空间内配置vs，转发至80。这样http可以直接访问.
3. 生产环境中，用的是托管eks集群。采用了token登录认证.

执行步骤
```
# 创建dashboard服务
kubectl apply -f dashboard-v2.7.0.yaml

# 创建dashboard的istio相关服务
kubectl apply -f dashboard-istio-gw.yaml
kubectl apply -f dashboard-istio-vs.yaml

# 创建dashboard的管理员账号admin
kubectl apply -f dashboard-admin.yaml
kubectl apply -f dashboard-admin-secret.yaml

# 取admin账号的token，登录dashboard
kubectl get secret admin -n kubernetes-dashboard -o jsonpath={".data.token"} | base64 -d
```
