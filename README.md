# demoK8Jenkins


# Master image (Execute inside master folder)
- sudo docker build -t gcr.io/plenary-ridge-120302/jenkins-master image/
- sudo gcloud docker push gcr.io/plenary-ridge-120302/jenkins-master

# Create the pod
- kubectl create -f pod_config.json

# Create the replication controller
kubectl create -f replication_controller_config.json

# Create the service
kubectl create -f service_config.json

# Describe the service
kubectl services describe jenkins

# Check the IP beside Ingress
# Access jenkins on http://<ip>:8080


# Slave image (Execute inside slave folder)
- sudo docker build -t gcr.io/plenary-ridge-120302/jenkins-cloud-sdk-slave slave/
- sudo gcloud docker push gcr.io/plenary-ridge-120302/jenkins-cloud-sdk-slave


# Run one slave [This command creates the pod + replication controller
kubectl run jenkins-cloud-sdk-slave --image=gcr.io/plenary-ridge-120302/jenkins-cloud-sdk-slave

# Scale 3 instances
kubectl scale rc jenkins-cloud-sdk-slave --replicas=3


