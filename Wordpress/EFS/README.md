# EFS
Criar EFS.

Instalando efs-utils
https://github.com/aws/efs-utils

Criando namespace
kubectl create namespace ns-k8s-teste-efs

Listando
kubectl get namespace

Deployment EFS create-efs-provisioner.yaml
kubectl apply -f create-efs-provisioner.yaml --namespace=ns-k8s-teste-efs


# RBAC reate-rbac.yaml

kubectl apply -f create-rbac.yaml --namespace=ns-k8s-teste-efs

# Create-storage.yaml

kubectl apply -f create-storage.yaml --namespace=ns-k8s-teste-efs

# Deployment Mysql
kubectl create secret generic mysql-pass --from-literal=password=eks-course-mysql-pw --namespace=ns-k8s-teste-efs
