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

# eksctl get cluster	

# kubectl get nodes

# eksctl get nodegroup --cluster teste-cluster

# eksctl delete cluster -f eks-teste.yaml

#  kubectl -n kube-system describe deployment cluster-autoscaler

# eksctl create cluster 'eks-teste.yaml --zones us-east-1a,us-east-1b,us-east-1c

# kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml

# kubectl -n kube-system annotate deployment.apps/cluster-autoscaler cluster-autoscaler.kubernetes.io/safe-to-evict="false"

# kubectl -n kube-system edit deployment.apps/cluster-autoscaler		-> 	altere o nome do cluster e versão
