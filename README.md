# Amazon EKS Cluster with Istio Blueprints 

This code shows how to provision an EKS cluster with Istio and some of EKS add-ons.

* Deploy EKS Cluster with one managed node group in an VPC
* Add node_security_group rules for port access required for Istio communication
* Install Istio using Helm resources in Terraform
* Install Istio Ingress Gateway using Helm resources in Terraform
  * This step deploys a Service of type `LoadBalancer` that creates an AWS Network Load Balancer.
* Deploy/Validate Istio communication using sample application

Refer to the [documentation](https://istio.io/latest/docs/concepts/) on Istio
concepts.

## Deploy

See [here](https://aws-ia.github.io/terraform-aws-eks-blueprints/getting-started/#prerequisites) for the prerequisites and run the following command to deploy this pattern.

```sh
terraform init
terraform apply --auto-approve
```

Once the resources have been provisioned, you will need to replace the `istio-ingress` pods due to a [`istiod` dependency issue](https://github.com/istio/istio/issues/35789). Use the following command to perform a rolling restart of the `istio-ingress` pods:

```sh
kubectl rollout restart deployment istio-ingress -n istio-ingress
```
