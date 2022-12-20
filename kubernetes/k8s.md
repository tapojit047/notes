Learned git
GO
Build an api server using GO









































Docker:
Steps for containerizing an application:
Create a file named docker file
Add instructions in docker fie
Build docker file to create image
Run image to create container

Docker commands:
Docker ps
List all the running containers

Docker images
List all the images in the computer

docker build -t go-docker .
Build a docker image from the dockerfile naming it go-docker

docker run -d -p 8080:8080 go-docker
Run the docker image “go-docker”(here the id of the image can be given as well) in detached mode with the port aligned with host 8080 and container 8080.

To push a docker image to docker hub: How to Push and Pull a Docker Image from Docker Hub



Kubernetes:
Deployment: A Kubernetes Deployment tells Kubernetes how to create or modify instances of the pods that hold a containerized application.


Commands:
Creating cluster: kind create cluster --wait 5m
Deleting cluster: kind delete cluster
Creating pods:    kubectl apply -f kuard-pod.yaml
Listing Pods:      kubectl get pods
Pod Details:        kubectl describe pods kuard
"kubectl  get pods -o wide" --> single line but more info
kubectl  get pods -o yaml
Deleting a Pod:   kubectl delete pods/kuard
Running Commands in Your Container with exec:
kubectl exec -it kuard -- ash
