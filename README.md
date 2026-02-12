Installation Guide -Docker Engine:
1.System Prep & Dependencies
sudo apt update
sudo apt upgrade -y
sudo apt install -y ca-certificates curl gnupg
2: Security Key Setup
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | \
sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
 sudo chmod a+r /etc/apt/keyrings/docker.gpg
3: Adding the Repository
echo \
  "deb [arch=$(dpkg --print-architecture) \
  signed-by=/etc/apt/keyrings/docker.gpg] \
https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo $VERSION_CODENAME) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
4: The Final Installation
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

Intallation Guide -Minikube
Minikube  is the industry standard tool for learning and developing Kubernetes locally,
without the expense or complexity of a full-scale cloud cluster.
1: Minikube Installation & Permissions
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
sudo usermod -aG docker $USER
newgrp docker
2: Starting the Cluster
now restart the ec2 instance
minikube start --driver=docker
3: Kubectl (The Controller) Installation
curl -LO https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
chmod +x kubectl
sudo mv kubectl /usr/local/bin/
kubectl version –client

Kubernetes
  It is a open-source orchestration platform
 Purpose: if docker is used to create the containers and then Kubernetes is the “Captain” of the ship. It ensures containers are running in the right place.
Commands:
kubectl get pods -n kube-system
this command displays all system-level pods required for Kubernetes to operate.
 
kubectl describe pod kube-apiserver-minikube -n kube-system
It provides a detailed report and event log of Kubernets API server, to check its configuration and troubleshooting issues.
kubectl run monisha-nginx --image=nginx
It creates and starts a single pod named “monisha-nginx” using Ngnix image to quickly deploy a web server
 
kubectl get pods
To display the list of the pods created, along with the current status, readiness and restart count.
 
kubectl delete pod monisha-nginx
Manually stops and deletes the particular Pod referred to as 'monisha-nginx' from the cluster.
 

kubectl create deployment monisha-nginx --image=nginx
It ensures the application stays running even when individual pods fail. It creates a deployment object which manages sets of Ngnix pods 
 
kubectl scale deployment monisha-ngnix  --replicas=5
It increases the number of running Ngnix pods to 5, in-order to handle more traffic
 
kubectl get pods
It shows the list of all active pods in the current namespace, their running status, readiness and restart count, and total time.
 
Kubectl get deployment
 
It displays the summary of all deployments in the namespace, Number of desired, up-to-date, available pod replicas currently running .
kubectl delete deployment monisha-nginx
This prompt permanently delete the deployment and all its managed pods.
 


YAML : Yet Another Markup Language
It’s a human readable data serialization language used for writing configuration files.
YAML is the language which allows you to specify exactly what the cluster wants to build, by writing requirements in file so that we can avoid lengthy commands.
vi ngnix-deployment	.yaml
It opens the vim text editor to create/modify a configuration for the file named as “ngnix-deployment” – define pods/deployment.
kubectl apply -f nginx-deployment.yaml
it instructs Kubernetes to read the configuration file & create/update the deployment exactly as mentioned in the YAML manifest.
 
Same as like different configuration file named as 
 ngnix-configmap.yaml 
                  ngnix-service.yaml
	         ngnix-secret.yaml was created.
 

To read the content of the file, the standard linux commands cat, used.
cat nginx-deployment.yaml
 cat nginx-service.yaml
cat nginx-secret.yaml

kubectl get svc 
To list all the services in the current namespace, it shows internal, external cluster IP, ports and age.
 

kubectl exec -it nginx-deployment-65d86b6f48-kjvtn -- /bin/bash
It enables you to troubleshoot/configure a particular container instance in real-time.
Opens a interactive bash shell inside a pod which managed by deployment.


