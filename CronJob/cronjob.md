# Cron Jobs

Ele agenda e executa tarefas periodicamente em um determinado cronograma.

    
    nano cronjob.yaml

```yaml
apiVersion: batch/v1beta1
kind: CronJob
metadata:
  name: giropops-cron
spec:
  schedule: "*/1 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
          - name: giropops-cron
            image: busybox
            args:
            - /bin/sh
            - -c
            - date; echo Bem Vindo ao Descomplicando Kubernetes - LinuxTips VAIIII ;sleep 30
          restartPolicy: OnFailure
```
   * Executando o Cronjob
          
          kubectl apply -f cronjob.yaml

  * Listar
  
          kubectl get cronjob.batch
  
          kubectl get jobs

* Verificando a saída do Cron

          kubectl get jobs --watch
