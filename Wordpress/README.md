# PVC

Listar todo os namespaces
kubectl get pods --all-namespaces

Criando namespace
kubectl create namespace ns-k8s-teste


kubectl get storageclasses --namespace=ns-k8s-teste

Deployment pvcs
kubectl apply -f pvcs.yaml --namespace=ns-k8s-teste


Listando 
kubectl get pvc --namespace=ns-k8s-teste

# Secret
Criando secret
kubectl create secret generic mysql-pass --from-literal=password=eks-course-mysql-pw --namespace=ns-k8s-teste

Listando secret
kubectl get secrets

kubectl get secret --namespace=ns-k8s-teste

#Deployment Mysql

kubectl apply -f deploy-mysql.yaml --namespace=ns-k8s-teste

kubectl get pods -o wide --namespace=ns-k8s-teste

# Deployment Wordpress

kubectl apply -f deploy-wordpress.yaml  --namespace=ns-k8s-teste


kubectl get pvc --namespace=ns-k8s-teste

