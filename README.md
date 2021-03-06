# EKS
* Download Pré requisito na EC2

AWS CLI
https://docs.aws.amazon.com/pt_br/cli/latest/userguide/install-cliv2-linux.html	
	

EKSCTL
https://docs.aws.amazon.com/pt_br/eks/latest/userguide/eksctl.html	
	

KUBECTL
https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/	


Criar um kubeconfig Amazon EKS
https://docs.aws.amazon.com/pt_br/eks/latest/userguide/create-kubeconfig.html

# Comandos

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

Coloque a anotação

	kubectl -n kube-system annotate deployment.apps/cluster-autoscaler cluster-autoscaler.kubernetes.io/safe-to-evict="false"

Editar a implantação e defina o nome do cluster

	kubectl -n kube-system edit deployment.apps/cluster-autoscaler

Dimensionar a implantação

	kubectl scale --replicas=3 deployment/test-autoscaler

Logs do autoscaler

	kubectl -n kube-system logs deployment.apps/cluster-autoscaler

Verificando pods

	kubectl get pods -o wide --watch

# Config Map

Criando arquivo config map e acresentando a credencial k8s-teste	
	
	kubectl -n kube-system get configmap aws-auth -o yaml > aws-auth-configmap.ymal

Executando config map

	kubectl apply -f aws-auth-configmap.ymal -n kube-system

Listando informações do aws-auth

	kubectl -n kube-system describe cm aws-auth  

Listando aws-auth

	kubectl -n kube-system get cm aws-auth  

Verificando qual credencial está sendo usada	

	aws sts get-caller-identity

Setando a credencial k8s-teste		
	
	export AWS_PROFILE="k8s-teste"

Criando namespace	

	kubectl create namespace production

# Implantar o autoescalador
	kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml


# estudo-01.yaml
 Criando o cluster		
 
 	eksctl cluster -f eks-teste.yaml

Log do Cloudwatch de um cluster EKS via arquivo de configuração yaml
	
	eksctl utils update-cluster-logging --config-file estudo-01.yaml --approve

Adicione política ao (s) seu (s) grupo (s) de nós. Adicione a política * CloudWatchAgentServerPolicy * à função do (s) grupo (s) de nó.

Deploy the cloudwatch agent

	curl https://raw.githubusercontent.com/aws-samples/amazon-cloudwatch-container-insights/master/k8s-yaml-templates/quickstart/cwagent-fluentd-quickstart.yaml | sed "s/{{cluster_name}}/teste-cluster/;s/{{region_name}}/us-east-1/" | kubectl apply -f -

Listar amazon-cloudwatch 

	kubectl get all -n amazon-cloudwatch

# estudo-02.yaml
## Ativar autoescalador de cluster

O autoescalador de cluster inicia automaticamente nós de trabalho adicionais se mais recursos forem necessários e desligará nós de trabalho se eles forem subutilizados. O escalonamento automático funciona dentro de um grupo de nós, portanto, crie primeiro um grupo de nós que tenha esse recurso habilitado.

Deploy

	kubectl apply -f estudo-o2.yaml
	
Deploy do autoscaler	

	kubectl apply -f https://raw.githubusercontent.com/kubernetes/autoscaler/master/cluster-autoscaler/cloudprovider/aws/examples/cluster-autoscaler-autodiscover.yaml

Coloque a anotação necessária para a implantação

	kubectl -n kube-system annotate deployment.apps/cluster-autoscaler cluster-autoscaler.kubernetes.io/safe-to-evict="false"

Edite a implantação e defina o nome do cluster EKS	

	kubectl -n kube-system edit deployment.apps/cluster-autoscaler

Defina a versão da imagem na propriedade 'image = k8s.gcr.io / cluster-autoscaler: vx.yy.z'
Defina o nome do cluster EKS no final da propriedade '- --node-group-auto-discovery = asg: tag = k8s.io / cluster-autoscaler / enabled, k8s.io / cluster-autoscaler / << EKS nome do cluster >>'

Listar os registros do autoescalador de cluster			

	kubectl -n kube-system logs deployment.apps/cluster-autoscaler

#  estudo-nginx-deployment.yaml
Deployment nginx	

	kubectl apply -f nginx-deployment.yaml
Dimensionar a implantação
	
	kubectl scale --replicas=3 deployment/test-autoscaler

