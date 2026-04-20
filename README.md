<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Deploy Backend with Kubernetes

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-compute-eks4)

**Author:** Gangadhar Shebannavar  
**Email:** gangadhar.shebannavar@gmail.com

---

## Deploy Backend with Kubernetes 

<img width="1511" height="790" alt="image" src="https://github.com/user-attachments/assets/9d51f657-4f52-4af3-982f-ed0034bdceef" />





![Image](http://learn.nextwork.org/motivated_teal_peaceful_coriander/uploads/aws-compute-eks4_6cfb382f2)

---

## Introducing Today's Project!

In this project, I will set up the backend of an application, install kubectl, and deploy the app on a Kubernetes cluster because I want to understand how to run and manage a containerized application on EKS. I will also track the deployment using EKS to see how the application is created and running inside the cluster.

### Tools and concepts

Key tools and concepts in this project included Amazon EKS for running the Kubernetes cluster, EC2 as the command machine, eksctl for creating the cluster, kubectl for managing resources, and Amazon ECR for storing the container image.

Important concepts included containers, pods, deployments, services, node groups, IAM roles and access, and how Kubernetes maintains the desired state and handles scaling and recovery.

### Project reflection

This project took me approximately 2–3 hours to complete. The most challenging part was fixing issues with eksctl setup, IAM permissions, and getting the correct port and security group configuration to access the application. My favourite part was seeing the application run successfully on Kubernetes and accessing it through the browser after setting up the Service.

---

## Project Set Up

### Kubernetes cluster

To set up today’s project, I launched a Kubernetes cluster using eksctl from my EC2 instance. The cluster’s role in this deployment is to run and manage my application by scheduling containers on worker nodes, handling scaling, and ensuring the application stays available.

### Backend code

I retrieved the backend code by cloning the repository from GitHub to my EC2 instance using Git.

Pulling code is essential to this deployment because it gives me the application files needed to build the container image and deploy the app to my Kubernetes cluster.

### Container image

Once I cloned the backend code, I built a container image because Kubernetes runs applications as containers, not raw code. Packaging the app into an image ensures everything it needs is included and runs the same way everywhere.

Without an image, it would be difficult for Kubernetes to deploy and run the application consistently across nodes.

I also pushed the container image to a container registry, which is a place to store and manage container images so they can be pulled when needed.

ECR facilitates scaling for my deployment because it allows multiple pods to pull the same image reliably, making it easy for Kubernetes to create and run more instances of the application when required.

---

## Manifest files

Kubernetes manifests are YAML files that define how resources like Pods, Deployments, and Services should be created and managed in a cluster.

Manifests are helpful because they let me describe my application setup in a clear way, so I can create the same setup again whenever needed without doing everything manually.

A Deployment manifest manages how my application runs in Kubernetes by defining the number of replicas, the container image, and how pods should be created and maintained.

The container image URL in my Deployment manifest tells Kubernetes where to pull the application image from (Amazon ECR in my case) so it can create and run the containers inside the cluster.

A Service resource exposes my application by providing a stable way to access pods, even if the pods restart or change.

My Service manifest sets up a NodePort that receives traffic on a fixed port and forwards it to the correct pods running my application, so I can access it from outside the cluster using the EC2 public IP.

![Image](http://learn.nextwork.org/motivated_teal_peaceful_coriander/uploads/aws-compute-eks4_b01876554)

---

## Backend Deployment!

To deploy my backend application, I applied my Deployment and Service manifests using kubectl, which created the pods and exposed the application so it could be accessed from outside the cluster.

### kubectl

kubectl is a command-line tool used to interact with a Kubernetes cluster.

I need this tool to deploy my application, check pods and services, and manage resources inside the cluster.

I can't use eksctl for this job because eksctl is mainly used to create and configure the EKS cluster, while kubectl is used to control and manage what runs inside it.


![Image](http://learn.nextwork.org/motivated_teal_peaceful_coriander/uploads/aws-compute-eks4_6cfb382f2)

---

## Verifying Deployment

My extension for this project is to use the EKS console to view and verify my cluster resources like nodes, pods, and services in a visual way.

I had to set up IAM access policies because, by default, I don’t have permission to access or manage the cluster from the console.

I set up access by creating an IAM access entry and granting my IAM identity the required permissions so I could view and interact with the cluster.

Once I gained access into my cluster's nodes, I discovered pods running inside each node. Pods are the smallest unit in Kubernetes that run one or more containers together.

Containers in a pod share the same network (IP and port space) and storage, which allows them to communicate easily with each other.

The EKS console shows you the events for each pod, where I could see steps like scheduling, pulling the container image from ECR, creating the container, and starting it.

This validated that my backend pod was successfully created, the image was pulled correctly, and the application started running without errors.

![Image](http://learn.nextwork.org/motivated_teal_peaceful_coriander/uploads/aws-compute-eks4_3b391f873)


