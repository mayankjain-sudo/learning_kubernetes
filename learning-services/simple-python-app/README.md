# Learning Kubernetes Services 

In this example we will learn Kubernetes service. This is simple python application which I copied from 
"https://github.com/iam-veeramalla/Docker-Zero-to-Hero/tree/main/examples/python-web-app"

But since the repo is old it will not work as aspected, we need some modification in the code.

1. When you try to build image locally from the Docker file from above link you will get below error \
    __This environment is externally managed__
    To fix the above error you need to add the below lines in the Dockerfile which I already added in my Dockerfile. \
    __rm /usr/lib/python*/EXTERNALLY-MANAGED &&__
2. When you try to run deployment you will face issue of "ImagePullBackOff" which cause no pods running.
    To fix the above issue you need to first add your local image which you created into minikube cluster since I am using minikube for my learning. You can add the image in minikube by running below command on your terminal. \
    __minikube cache add ImageName__ \
    __Note:__ "minikube cache" will be deprecated in upcoming versions, please switch to __minikube image load__

## Commands used in this project 
    > kubectl apply -f deployment.yaml
    > kubectl get deployments
    > kubectl apply -f service.yaml
    > kubectl get svc

Once the service is up now we will access the service via cluster IP address in our local.

Since I am using minikube you can refer here : https://minikube.sigs.k8s.io/docs/handbook/accessing/ to learn how to access your application.

***minikube service <service-name> --url*** runs as a process, creating a tunnel to the cluster. The command exposes the service directly to any program running on the host operating system.

# output
    > mayankjain@Mayanks-Laptop learning-services % minikube service python-app-service --url  
        http://127.0.0.1:60003
        ❗  Because you are using a Docker driver on darwin, the terminal needs to be open to run it.

# Check ssh tunnel in another terminal
    > ps -ef | grep docker@127.0.0.1
      ssh -o UserKnownHostsFile=/dev/null -o StrictHostKeyChecking=no -N docker@127.0.0.1 -p 55972 -i /Users/FOO/.minikube/machines/minikube/id_rsa -L TUNNEL_PORT:CLUSTER_IP:TARGET_PORT

  
In my case Tunner port is 60003

Try in your browser
> Open in your browser (ensure there is no proxy set)
    http://127.0.0.1:TUNNEL_PORT
