#####  创建 2个pod



···

kubectl apply -f nginx-nfs.yaml

···







#####  创建 ingress svc



···

kubectl apply -f  service-nodeport.yaml

···







#####  创建 ingress rule



···

kubectl apply -f ingress-web.yaml

···





