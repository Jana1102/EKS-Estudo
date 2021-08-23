# Limitando recursos de um namespace especifico


Criando namespace que será limitado
		
    kubectl create namespace primeiro-namespace

Criando limitando-recursos.yaml que fará a limitação dos recursos para o namespace primeiro-namespace

		kubectl create -f limitando-recursos.yaml --namespace=primeiro-namespace

Listando
	
    kubectl describe limitranges --namespace=primeiro-namespace limitando-recursos

Criando pod-limitado.yaml que vai ser limitado devido está com namespace primeiro-namespace

		kubectl apply -f pod-limitado.yaml --namespace=primeiro-namespace

Listando o pod que está usando limitRange

    kubectl get pods --namespace=primeiro-namespace



