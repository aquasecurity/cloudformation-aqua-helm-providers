# Aqua resource types for AWS CloudFormation

AWS CloudFormation resource types for the management of aqua in EKS and self-managed Kubernetes clusters.

## Prerequisites

### IAM role
An IAM role is used by CloudFormation to execute the resource type handler code.
A CloudFormation template to create the execution role is available
[here](https://github.com/aws-quickstart/quickstart-helm-resource-provider/blob/main/execution-role.template.yaml)

### Create an EKS cluster and provide CloudFormation access to the Kubernetes API
EKS clusters use IAM to allow access to the kubernetes API, as the CloudFormation resource types in this project
interact with the kubernetes API, the IAM execution role must be granted access to the kubernetes API. This can be done
in one of two ways:
* Create the cluster using CloudFormation: Currently there is no native way to manage EKS auth using CloudFormation
  (+1 [this GitHub issue](https://github.com/aws/containers-roadmap/issues/554) to help prioritize native support).
  For this reason `AWSQS::EKS::Cluster` has been published. Instructions on activation and usage can be found
  [here](https://github.com/aws-quickstart/quickstart-amazon-eks-cluster-resource-provider/blob/main/README.md).
* Manually: to allow this resource type to access the kubernetes API, follow the
  [instructions in the EKS documentation](https://docs.aws.amazon.com/eks/latest/userguide/add-user-role.html) adding
  the IAM execution role created above to the `system:masters` group. (Note: you can scope this down if you plan to use
  the resource type to only perform specific operations on the kubernetes cluster)

## Activating the Resource types
To activate the resource types in your account follow the links below, then choose the AWS Region you would like to use it in and click ***Activate***.
* [`Aqua::Enterprise::Server`](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/registry/public-extensions/details/schema?arn=arn:aws:cloudformation:us-east-1::type/resource/4f06bc39af5f4b984dd46ad17f10316e6258d9fa/Aqua-Enterprise-Server)
* [`Aqua::Enterprise::Enforcer`](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/registry/public-extensions/details/schema?arn=arn:aws:cloudformation:us-east-1::type/resource/4f06bc39af5f4b984dd46ad17f10316e6258d9fa/Aqua-Enterprise-Enforcer)
* [`Aqua::Enterprise::KubeEnforcer`](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/registry/public-extensions/details/schema?arn=arn:aws:cloudformation:us-east-1::type/resource/4f06bc39af5f4b984dd46ad17f10316e6258d9fa/Aqua-Enterprise-KubeEnforcer)
* [`Aqua::Enterprise::Scanner`](https://console.aws.amazon.com/cloudformation/home?region=us-east-1#/registry/public-extensions/details/schema?arn=arn:aws:cloudformation:us-east-1::type/resource/4f06bc39af5f4b984dd46ad17f10316e6258d9fa/Aqua-Enterprise-Scanner)

## Usage
* `Aqua::Enterprise::Server` - [CloudFormation properties](./aqua-enterprise-server/docs/README.md) - [Helm values](https://github.com/aquasecurity/aqua-helm/tree/6.0/server#configurable-variables)
* `Aqua::Enterprise::Enforcer` - [CloudFormation properties](./aqua-enterprise-enforcer/docs/README.md) - [Helm values](https://github.com/aquasecurity/aqua-helm/tree/6.0/kube-enforcer#configurable-variables)
* `Aqua::Enterprise::KubeEnforcer` - [CloudFormation properties](./aqua-enterprise-kubeenforcer/docs/README.md) - [Helm values](https://github.com/aquasecurity/aqua-helm/tree/6.0/server#configurable-variables)
* `Aqua::Enterprise::Scanner` - [CloudFormation properties](./aqua-enterprise-scanner/docs/README.md) - [Helm values](https://github.com/aquasecurity/aqua-helm/tree/6.0/scanner#configurable-variables)

