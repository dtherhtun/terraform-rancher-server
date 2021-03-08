# Rancher server Terraform module

Terraform module which creates servers to host Rancher and installs Rancher on them.

To use this module, you must [install the RKE provider](https://github.com/yamamoto-febc/terraform-provider-rke#installation).

## Terraform versions

Terraform 0.12

## Usage

```hcl
module "rancher_server" {
  rancher_password           = var.rancher_password
  use_default_vpc            = false
  vpc_id                     = "vpc-foobar"
  aws_region                 = "us-east-1"
  aws_profile                = null
  aws_elb_subnet_ids         = ["subnet-1", "subnet-2"]
  domain                     = "foo.domain"
  r53_domain                 = "rancher.foo.domain"
  rancher2_master_subnet_ids = ["subnet-1", "subnet-2"]
  rancher2_worker_subnet_ids = ["subnet-1", "subnet-2"]

  providers = {
    aws     = "aws"
    aws.r53 = "aws.r53"
  }
}
```
<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Requirements

| Name | Version |
|------|---------|
| terraform | >= 0.13 |
| helm | 1.3.2 |
| k8s | 0.8.2 |
| local | 2.0.0 |
| rancher2 | 1.10.6 |
| rke | 1.1.6 |

## Providers

| Name | Version |
|------|---------|
| aws | n/a |
| aws.r53 | n/a |
| helm | 1.3.2 |
| local | 2.0.0 |
| null | n/a |
| rancher2 | 1.10.6 |
| rancher2.bootstrap | 1.10.6 |
| rke | 1.1.6 |
| tls | n/a |

## Modules

No Modules.

## Resources

| Name |
|------|
| [aws_ami](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/ami) |
| [aws_autoscaling_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/autoscaling_group) |
| [aws_elb](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/elb) |
| [aws_iam_access_key](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_access_key) |
| [aws_iam_user](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user) |
| [aws_iam_user_policy](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/iam_user_policy) |
| [aws_instance](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/instance) |
| [aws_instances](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/instances) |
| [aws_key_pair](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/key_pair) |
| [aws_launch_template](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/launch_template) |
| [aws_lb](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb) |
| [aws_lb_listener](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_listener) |
| [aws_lb_target_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_target_group) |
| [aws_lb_target_group_attachment](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/lb_target_group_attachment) |
| [aws_route53_record](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/route53_record) |
| [aws_route53_zone](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/route53_zone) |
| [aws_s3_bucket](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/s3_bucket) |
| [aws_security_group](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/security_group) |
| [aws_subnet_ids](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/subnet_ids) |
| [aws_vpc](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/vpc) |
| [helm_release](https://registry.terraform.io/providers/hashicorp/helm/1.3.2/docs/resources/release) |
| [helm_repository](https://registry.terraform.io/providers/hashicorp/helm/1.3.2/docs/data-sources/repository) |
| [local_file](https://registry.terraform.io/providers/hashicorp/local/2.0.0/docs/resources/file) |
| [null_resource](https://registry.terraform.io/providers/hashicorp/null/latest/docs/resources/resource) |
| [rancher2_auth_config_github](https://registry.terraform.io/providers/rancher/rancher2/1.10.6/docs/resources/auth_config_github) |
| [rancher2_bootstrap](https://registry.terraform.io/providers/rancher/rancher2/1.10.6/docs/resources/bootstrap) |
| [rancher2_user](https://registry.terraform.io/providers/rancher/rancher2/1.10.6/docs/data-sources/user) |
| [rke_cluster](https://registry.terraform.io/providers/rancher/rke/1.1.6/docs/resources/cluster) |
| [tls_private_key](https://registry.terraform.io/providers/hashicorp/tls/latest/docs/resources/private_key) |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| aws\_elb\_subnet\_ids | List of subnet ids in which to place the AWS ELB | `list(any)` | `[]` | no |
| aws\_profile | n/a | `string` | `"rancher-eng"` | no |
| aws\_region | n/a | `string` | `"us-west-2"` | no |
| certmanager\_chart | Helm chart to use for cert-manager install | `string` | `"jetstack/cert-manager"` | no |
| certmanager\_version | Version of cert-manager to install | `string` | `"0.10.0"` | no |
| creds\_output\_path | Where to save the id\_rsa config file. Should end in a forward slash `/` . | `string` | `"./"` | no |
| domain | n/a | `string` | `"eng.rancher.space"` | no |
| extra\_ssh\_keys | Extra ssh keys to inject into Rancher instances | `list(any)` | `[]` | no |
| github\_client\_id | GitHub client ID for Rancher to use, if using GH auth | `string` | `""` | no |
| github\_client\_secret | GitHub client secret for Rancher to use, if using GH auth | `string` | `""` | no |
| instance\_ssh\_user | Username for sshing into instances | `string` | `"ubuntu"` | no |
| instance\_type | n/a | `string` | `"t3.large"` | no |
| le\_email | LetsEncrypt email address to use | `string` | `"none@none.com"` | no |
| master\_node\_count | Number of master nodes to launch | `number` | `3` | no |
| name | Name for deployment | `string` | `"rancher-demo"` | no |
| r53\_domain | DNS domain for Route53 zone (defaults to domain if unset) | `string` | `""` | no |
| rancher2\_custom\_tags | Custom tags for Rancher resources | `map(any)` | <pre>{<br>  "DoNotDelete": "true",<br>  "Owner": "EIO_Demo"<br>}</pre> | no |
| rancher2\_extra\_allowed\_gh\_principals | List of principals in form github\_user://IDNUM to be given Rancher access | `list(any)` | `[]` | no |
| rancher2\_github\_auth\_enabled | Whether to use GitHub authentication for Rancher | `bool` | `false` | no |
| rancher2\_github\_auth\_org | GitHub numerical ID of organization to grant Rancher access to | `string` | `"53273206"` | no |
| rancher2\_github\_auth\_team | GitHub numerical ID of team to grant Rancher access to | `string` | `"3414845"` | no |
| rancher2\_github\_auth\_user | GitHub numerical ID of user to grant Rancher access to | `string` | `"3430214"` | no |
| rancher2\_master\_custom\_tags | Custom tags for Rancher master nodes | `map(any)` | `{}` | no |
| rancher2\_master\_subnet\_ids | List of subnet ids for Rancher master nodes | `list(any)` | `[]` | no |
| rancher2\_worker\_custom\_tags | Custom tags for Rancher worker nodes | `map(any)` | `{}` | no |
| rancher2\_worker\_subnet\_ids | List of subnet ids for Rancher worker nodes | `list(any)` | `[]` | no |
| rancher\_chart | Helm chart to use for Rancher install | `string` | `"rancher-stable/rancher"` | no |
| rancher\_current\_password | Rancher admin user current password | `string` | `null` | no |
| rancher\_nodes\_in\_asgs | Control whether to put Rancher nodes in ASGs | `bool` | `true` | no |
| rancher\_password | Password to set for Rancher root user | `string` | n/a | yes |
| rancher\_version | Version of Rancher to install | `string` | `"2.2.9"` | no |
| rke\_backups\_region | Region to perform backups to S3 in. Defaults to aws\_region | `string` | `""` | no |
| rke\_backups\_s3\_endpoint | Override for S3 endpoint to use for backups | `string` | `""` | no |
| use\_default\_vpc | Should the default VPC for the region selected be used for Rancher | `bool` | `true` | no |
| vpc\_id | If use\_default\_vpc is false, the vpc id that Rancher should use | `string` | `null` | no |
| worker\_node\_count | Number of worker nodes to launch | `number` | `3` | no |

## Outputs

| Name | Description |
|------|-------------|
| etcd\_backup\_s3\_bucket\_id | S3 bucket ID for etcd backups |
| etcd\_backup\_user\_key | AWS IAM access key id for etcd backup user |
| etcd\_backup\_user\_secret | AWS IAM secret access key for etcd backup user |
| master\_addresses | IP addresses of Rancher master nodes |
| rancher\_admin\_password | Password set for Rancher local admin user |
| rancher\_api\_url | FQDN of Rancher's Kubernetes API endpoint |
| rancher\_token | Admin token for Rancher cluster use |
| rancher\_url | URL at which to reach Rancher |
| worker\_addresses | IP addresses of Rancher worker nodes |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
