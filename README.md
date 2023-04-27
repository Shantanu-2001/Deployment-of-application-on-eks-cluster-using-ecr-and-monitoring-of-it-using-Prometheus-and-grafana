# Deployment-of-application-on-eks-cluster-using-ecr-and-monitoring-of-it-using-Prometheus-and-grafana

Deploying an application on Amazon Elastic Kubernetes Service (EKS) using Elastic Container Registry (ECR) and monitoring it with Prometheus and Grafana involves several steps. Here's a high-level overview of the process:

1. Create an ECR repository: First, create a repository in ECR to store the Docker image of your application.

2. Build and push Docker image: Build a Docker image of your application and push it to the ECR repository.

3. Create an EKS cluster: Create an EKS cluster using the AWS Management Console or AWS CLI.

4. Create a Kubernetes deployment: Create a Kubernetes deployment manifest file for your application.

5. Create a Kubernetes service: Create a Kubernetes service manifest file to expose your application.

6. Deploy the application: Use kubectl to deploy your application on the EKS cluster.

7. Install Prometheus and Grafana: Install Prometheus and Grafana on the EKS cluster.

8. Configure Prometheus: Configure Prometheus to scrape metrics from your application.

9. Configure Grafana: Configure Grafana to display the metrics collected by Prometheus.

10. Access the Grafana dashboard: Access the Grafana dashboard to view the metrics and monitor your application.

These steps provide a high-level overview of the process. However, the actual implementation may vary based on your specific requirements and application. It's recommended to follow the documentation provided by AWS and Kubernetes to ensure proper implementation.


## For Docker Installation
sudo apt-get update
sudo apt-get install docker.io -y
sudo usermod -aG docker $USER && newgrp docker

## aws cli
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install

## CloudFormation URL for creating VPC stack
https://amazon-eks.s3.us-west-2.amazonaws.com/cloudformation/2020-06-10/amazon-eks-vpc-private-subnets.yaml

## eksctl
ARCH=amd64 PLATFORM=$(uname -s)_$ARCH

curl -sLO "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$PLATFORM.tar.gz"

tar -xzf eksctl_$PLATFORM.tar.gz -C /tmp && rm eksctl_$PLATFORM.tar.gz

sudo mv /tmp/eksctl /usr/local/bin

## kubectl
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

kubectl version --client

## aws-iam-authenticator 
curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.9/aws-iam-authenticator_0.5.9_linux_amd64

chmod +x ./aws-iam-authenticator

mkdir -p $HOME/bin && cp ./aws-iam-authenticator $HOME/bin/aws-iam-authenticator && export PATH=$PATH:$HOME/bin

echo 'export PATH=$PATH:$HOME/bin' >> ~/.bashrc

aws-iam-authenticator help
