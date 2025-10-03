choco install eksctl

eksctl version

eksctl create cluster --name mycluster --region us-east-1

eksctl create cluster \
--name mycluster \
--region us-east-1 \
--nodegroup-name mynodes \
--node-type t3.medium \
--nodes 2 \
--nodes-min 2 \
--nodes-max 2 \
--managed

eksctl create cluster --name mycluster --region us-east-1 --nodegroup-name mynodes --node-type t3.medium --nodes 2 --nodes-min 2 --nodes-max 2 --managed

git clone https://github.com/atulkamble/docker-hello-world.git
cd docker-hello-world/k8s 

kubectl apply -f eks-deployment.yaml
kubectl apply -f eks-service.yaml

kubectl get pods 
kubectl get services 
kubectl get deployments

kubecl get service hello-web-svc

eksctl delete cluster --name mycluster --region us-east-1
