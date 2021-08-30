# HPA
		Deploy Metrics
		kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/download/v0.3.6/components.yaml
		
		Listando	
		kubectl get pods -n kube-system -l k8s-app=metrics-server
		
		
		 Criando umaa implantação php-apache
		 kubectl create deployment php-apache --image=k8s.gcr.io/hpa-example


	
		Para definir as solicitações da CPU, execute o seguinte comando. Se você não definir o valor da cpu corretamente, a métrica de utilização da CPU para o pod não está definida e o HPA não pode ser escalado.
		kubectl patch deployment php-apache -p='{"spec":{"template":{"spec":{"containers":[{"name":"hpa-example","resources":{"requests":{"cpu":"200m"}}}]}}}}'
		
		
		
		Para expor a implantação como um serviço, execute o seguinte comando
		kubectl create service clusterip php-apache --tcp=80
		
		
		
		Para criar um HPA, execute o seguinte comando
		kubectl autoscale deployment php-apache --cpu-percent=50 --min=1 --max=10
		
		Listando o HPA
		kubectl get hpa

