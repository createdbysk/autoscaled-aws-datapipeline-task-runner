# autoscaled-aws-datapipeline-task-runner
This repository provides a helm chart to deploy AWS Datapipeline task-runner instances on Kubernetes that autoscale based on configured utilization.


# Pre-requisites
## Install helm
#### Mac OSX

    brew install kubernetes-helm
    brew cask install minikube


# How-to

    git clone satvidh/autoscaled-aws-datapipeline-task-runner
    export S3_LOCATION_FOR_LOGS=<s3_location_for_logs>

*NOTE* Replace <s3_location_for_logs> with a location of the form ```s3://<your_s3_bucket>[/optional_prefix]```


    helm install horizontally_scaled_task_runner --set AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID,AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY,AWS_SESSION_TOKEN=$AWS_SESSION_TOKEN,WORKER_GROUP=scaled-task-runner,LOG_URI=${S3_LOCATION_FOR_LOGS}/datapipeline-logs --debug


# Minikube for local development
This is a one time setup step.

* If minikube is already running, then

      minikube stop

* Setup minikube for larger capacity and to enable the metrics-server to allow kubernetes to horizontally scale.

      minikube config set cpus 4
      minikube config set memory 8192
      minikube start -v=5
      minikube addons enable metrics-server
