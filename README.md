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

kubectl get pods

eksctl get cluster	

kubectl get nodes

eksctl get nodegroup --cluster teste-cluster

eksctl delete cluster -f eks-teste.yaml

kubectl -n kube-system describe deployment cluster-autoscaler

eksctl create cluster 'eks-teste.yaml --zones us-east-1a,us-east-1b,us-east-1c

kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml

kubectl -n kube-system annotate deployment.apps/cluster-autoscaler cluster-autoscaler.kubernetes.io/safe-to-evict="false"

kubectl -n kube-system edit deployment.apps/cluster-autoscaler

kubectl scale --replicas=3 deployment/test-autoscaler

kubectl -n kube-system logs deployment.apps/cluster-autoscaler

# estudo-01.yaml

 Criando cluster
  eksctl cluster -f eks-teste.yaml

 Cloudwatch logging of an EKS cluster
 enable e.g. via yaml config file

 eksctl utils update-cluster-logging --config-file eks-course.yaml --approve

add policy to your nodegroup(s)
add policy *CloudWatchAgentServerPolicy* to nodegroup(s) role

deploy the cloudwatch agent
curl https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/master/k8s-yaml-templates/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/teste-cluster/;s/{{region_name}}/us-east-1/" | kubectl apply -f -

Listar 
kubectl get all -n amazon-cloudwatch
