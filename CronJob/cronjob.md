kubectl apply -f cronjob.yaml

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
          - name: mensagegm-cron
            image: busybox
            args:
            - /bin/sh
            - -c
            - date; echo Bem Vindo ao Descomplicando Kubernetes - ;sleep 30
          restartPolicy: OnFailure

kubectl get cronjob.batch

kubectl get jobs

kubectl get jobs