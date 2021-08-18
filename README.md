# kubernetes
----Download Pré requisito na EC2---

AWS CLI
https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2-linux.html	
	

EKSCTL
https://docs.aws.amazon.com/pt_br/eks/latest/userguide/eksctl.html	
	

KUBECTL
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/	


Criar um kubeconfig Amazon EKS
https://docs.aws.amazon.com/pt_br/eks/latest/userguide/create-kubeconfig.html

-----Comandos-------

Listar pods
kubectl get pods

Listar Cluster
eksctl get cluster	

Listar Nodes
kubectl get nodes

Listar nodegroup

eksctl get nodegroup --cluster teste-cluster

Deletar cluster

eksctl delete cluster -f eks-teste.yaml

Mostrar detalhes do cluster-autoscaler, namespace kube-system.

kubectl -n kube-system describe deployment cluster-autoscaler

coloque a anotação necessária para a implantação
kubectl -n kube-system annotate deployment.apps/cluster-autoscaler cluster-autoscaler.kubernetes.io/safe-to-evict="false"

Edite a implantação e defina o nome do cluster
kubectl -n kube-system edit deployment.apps/cluster-autoscaler

Dimensionar a implantação
kubectl scale --replicas=3 deployment/test-autoscaler

Logs do autoscaler
kubectl -n kube-system logs deployment.apps/cluster-autoscaler

kubectl get pods -o wide --watch

# Implantar o autoescalador
kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml


# estudo-01.yaml
 Criando o cluster
 eksctl cluster -f eks-teste.yaml

 Cloudwatch logging of an EKS cluster via yaml config file
 
 eksctl utils update-cluster-logging --config-file eks-course.yaml --approve

add policy to your nodegroup(s)
add policy *CloudWatchAgentServerPolicy* to nodegroup(s) role

deploy the cloudwatch agent
curl https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/master/k8s-yaml-templates/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/teste-cluster/;s/{{region_name}}/us-east-1/" | kubectl apply -f -

Listar 
kubectl get all -n amazon-cloudwatch
