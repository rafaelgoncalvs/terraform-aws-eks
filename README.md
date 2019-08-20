# AWS EKS Infra using Terraform

## Apply configuration

This will initialize Terraform, creating the state file to track our work:
```
terraform init
```

To see a detailed outline of the changes Terraform would make, run plan:
```
terraform plan
```

To run the configuration against AWS:
```
terraform apply
```

This apply step will create many of the resources you need to get up and running initially, including:

- VPC
- IAM roles
- Security groups
- An internet gateway
- Subnets
- Autoscaling group
- Route table
- EKS cluster
- Your kubectl configuration

## Iteract with the cluster
To config your kubectl to interact with the EKS cluster:

```
mkdir ~/.kube/
```
```
terraform output kubeconfig>~/.kube/config
```


To add the ConfigMap to the cluster to grant access to the EKS cluster:

```
terraform output config_map_aws_auth > configmap.yml
```
```
kubectl apply -f configmap.yml
```

See if the two nodes has joined to the cluster:
```
kubectl get nodes -o wide
```

At this point, your EKS cluster is up, the nodes have joined, and they are ready for a deployment!

