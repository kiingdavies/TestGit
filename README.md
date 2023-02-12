# TestGit
This is for testing git


# Flask Application Deployment in Kubernetes
Before we begin, you can find the final images of the successfully built flask app "Hello world" page, the "Healthy" health-check page and the running container in the images folder.

This document explains the steps to deploy the Flask application in a Kubernetes cluster, incorporating a health-check URL to monitor the health of the application.

# Prerequisites
- A working Kubernetes cluster
- Docker installed on the system
- A Docker registry accessible to the Kubernetes cluster
- The Flask application code

# Steps
1. Add the health-check endpoint to the Flask application

In this step, I added a health-check endpoint to the Flask application that returns a 200 Healthy response when the application is healthy.

2. Build and push the Docker image to a registry eg Docker hub or Azure Container Registry
Once the health-check endpoint has been added and the Docker image is built and pushed to a registry that is accessible to the Kubernetes cluster.

Use the commands below to build an dpush the docker image:
docker build -t <image_name>:<tag> .
docker push <image_name>:<tag>

3. Update the Kubernetes Deployment
I will now update the company's already existing Kubernetes manifest deployment YAML file to add the health-check URL to the Pod specification. Here I used a readiness probe to check the health of the application. The readiness probe will determine if the application is ready to handle incoming requests. If the readiness probe fails, the Pod will be restarted.

In my config.yml file, the readiness probe will perform an HTTP GET request to /health on port 5000 every 5 seconds. If the health check fails, the Pod will be restarted.

4. Deploy the updated Kubernetes manifest file
Here you can apply the updated deployment YAML file to the cluster to deploy the updated Flask application with the health-check URL using the kubectl command below:

kubectl apply -f deployment.yaml

5. Monitor the health of the application
Lastly, you can monitor the health of the application by checking the logs of the pod running the Flask container. You can use tools like Prometheus and Grafana to monitor the health of the application and the health of the entire cluster.

