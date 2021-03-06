# terraform-aws-eks-base

[![Build Status](https://img.shields.io/circleci/build/github/qaifmz/terraform-aws-eks-base?style=for-the-badge)](https://github.com/qaifmz/terraform-aws-eks-base)
[![open-issues](https://img.shields.io/github/issues-raw/qaifmz/terraform-aws-eks-base?style=for-the-badge)](https://github.com/insight-infrastructure/terraform-aws-eks-base/issues)
[![open-pr](https://img.shields.io/github/issues-pr-raw/qaifmz/terraform-aws-eks-base?style=for-the-badge)](https://github.com/insight-infrastructure/terraform-aws-eks-base/pulls)

## Features

This module sets up a network and EKS cluster on AWS.  This is a simple base module that you can wrap from other 
modules or take the outputs from and use in adjacent modules. 

## Terraform Versions

For Terraform v0.12.24+

## Usage

```
module "this" {
  source = "github.com/qaifmz/terraform-aws-eks-base"
  id = "awesome-cluster-id"
}
```

## Instructions

You will need to configure your AWS credentials before using this project:

### Linux
Add the following in your `~/.bashrc` or `~/.zshrc` with your credentials:
```
export AWS_ACCESS_KEY_ID=YOUR_AWS_ACCESS_KEY_ID
export AWS_SECRET_ACCESS_KEY=YOUR_AWS_SECRET_ACCESS_KEY
```

### Windows
Execute the following in your terminal:
```
$ aws configure
AWS Access Key ID [None]: YOUR_AWS_ACCESS_KEY_ID
AWS Secret Access Key [None]: YOUR_AWS_SECRET_ACCESS_KEY
Default region name [None]: us-west-2
Default output format [None]: json
```

### Testing the Project

Initialize and Run Terraform Scripts
```
terraform init
terraform apply
```
Input Cluster name = `"cluster_name"` and input your choice of AWS Region: `us-west-2`

If the output gives connection errors, input the following commands:
```
aws eks --region us-west-2 update-kubeconfig --name cluster_name
terraform apply
```

## Examples

- [defaults](https://github.com/insight-infrastructure/terraform-aws-eks-base/tree/master/examples/defaults)

## Known  Issues
No issue is creating limit on this module.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| aws | n/a |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| azs | List of availability zones | `list(string)` | `[]` | no |
| cidr | The cidr range for network | `string` | `"10.0.0.0/16"` | no |
| cluster\_autoscale | Do you want the cluster's worker pool to autoscale? | `bool` | `true` | no |
| cluster\_autoscale\_max\_workers | Maximum number of workers in worker pool | `number` | `4` | no |
| cluster\_autoscale\_min\_workers | Minimum number of workers in worker pool | `number` | `1` | no |
| create | Bool to create | `bool` | `true` | no |
| id | The id of the resources | `string` | n/a | yes |
| num\_azs | The number of AZs to deploy into | `number` | `3` | no |
| num\_workers | Number of workers for worker pool | `number` | `1` | no |
| tags | Tags for resources | `map(string)` | `{}` | no |
| vpc\_name | The name of the VPC | `string` | `""` | no |
| worker\_instance\_type | The instance class for workers | `string` | `"m5.2xlarge"` | no |

## Outputs

| Name | Description |
|------|-------------|
| cluster\_arn | The Amazon Resource Name (ARN) of the cluster. |
| cluster\_certificate\_authority\_data | Nested attribute containing certificate-authority-data for your cluster. This is the base64 encoded certificate data required to communicate with your cluster. |
| cluster\_endpoint | The endpoint for your EKS Kubernetes API. |
| cluster\_id | The name/id of the EKS cluster. |
| cluster\_security\_group\_id | Security group ID attached to the EKS cluster. |
| cluster\_version | The Kubernetes server version for the EKS cluster. |
| config\_map\_aws\_auth | A kubernetes configuration to authenticate to this EKS cluster. |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Testing
This module has been packaged with terratest tests

To run them:

1. Install Go
2. Run `make test-init` from the root of this repo
3. Run `make test` again from root

## Authors

Module managed by [qaifmz](https://github.com/qaifmz)

## Credits

- [insight-infrastructure](https://github.com/insight-infrastructure)
- [Anton Babenko](https://github.com/antonbabenko)

## License

Apache 2 Licensed. See LICENSE for full details.
