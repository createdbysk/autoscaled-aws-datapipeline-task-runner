# horizontally-scale-data-pipelines
What it says.

# Ideas to try
## Change replicas to 0 rather than an entire helm install
* Deploy with an initial number of replicas equal to 0.
* When the workflow starts, raise the number to 1.
* When the workflow terminates, reduce the number to 0.

# Install helm
# Mac OSx

    brew install kubernetes-helm
    brew cask install minikube

# Run in kubernetes
    export S3_LOCATION_FOR_LOGS=<s3_location_for_logs>

*NOTE* Replace <s3_location_for_logs> with a location of the form ```s3://<your_s3_bucket>[/optional_prefix]```


    helm install horizontally_scaled_task_runner --set AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY_ID,AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY,AWS_SESSION_TOKEN=$AWS_SESSION_TOKEN,WORKER_GROUP=scaled-task-runner,LOG_URI=${S3_LOCATION_FOR_LOGS}/datapipeline-logs --debug


# Minikube

      minikube config set cpus 4
      minikube config set memory 8192
      minikube start -v=5
      minikube addons enable metrics-server
