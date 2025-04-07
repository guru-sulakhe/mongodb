# MongoDB

We use bastion host as Docker server and EKS client.
Make sure `aws configure` is done in bastion and connected to EKS cluster.
```
aws eks update-kubeconfig --region us-east-1 --name roboshop-dev
```
```
kubectl create namespace roboshop
```
* Login to ECR
```
git clone https://github.com/guru-sulakhe/mongodb.git
cd mongodb/
aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin 637423540068.dkr.ecr.us-east-1.amazonaws.com
```
* Build MongoDB image.
```
docker build -t 637423540068.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/mongodb:v1.0.2 .
```
* Push image
```
docker push 637423540068.dkr.ecr.us-east-1.amazonaws.com/roboshop/dev/mongodb:v1.0.2
```
* Now install using Helm. move to helm directory
```
helm upgrade --install mongodb . -n roboshop
```
