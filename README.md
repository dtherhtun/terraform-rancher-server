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
| terraform | ~> v0.13.4 |
| aws | ~> 3.16.0 |
| kubernetes | ~> 1.9 |
| kubernetes | >= 1.13.3 |
| local | ~> 2.0.0 |
| null | ~> 2.1 |
| random | ~> 3.0.0 |
| template | ~> 2.1 |
| tls | ~> 3.0.0 |

## Providers

| Name | Version |
|------|---------|
| aws | ~> 3.16.0 |
| local | ~> 2.0.0 |
| random | ~> 3.0.0 |
| tls | ~> 3.0.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| alb | n/a | <pre>object({<br>    cluster_type = string<br>    namespace    = string<br>  })</pre> | n/a | yes |
| aws\_access\_key | n/a | `string` | n/a | yes |
| aws\_secret\_key | n/a | `string` | n/a | yes |
| domain | External DNS | `string` | n/a | yes |
| eks | AWS EKS Variables | <pre>object({<br>    cluster_version         = string<br>    override_instance_types = list(string)<br>    spot_instance_pools     = number<br>    asg_max_size            = number<br>    is_public_ip            = bool<br>    asg_desire_cap          = number<br>    map_users               = list(object({ userarn = string, username = string, groups = list(string) }))<br>    map_accounts            = list(string)<br><br>  })</pre> | n/a | yes |
| key\_name | AWS Key\_pair variables | `string` | n/a | yes |
| rds | n/a | <pre>object({<br>    engine         = string<br>    engine_version = string<br>    instance_class = string<br>    storage        = string<br>    db_name        = string<br>    db_username    = string<br>    db_password    = string<br>    db_port        = string<br>    family         = string<br>    option         = string<br>    deletion       = bool<br>    maintenance    = string<br>    backup         = string<br>  })</pre> | n/a | yes |
| region | AWS Region | `string` | `"ap-southeast-1"` | no |
| vpc | AWS VPC Variables | <pre>object({<br>    cidr                = string<br>    azs                 = list(string)<br>    pri_sub             = list(string)<br>    pub_sub             = list(string)<br>    database_sub        = list(string)<br>    is_enable_natgw     = bool<br>    is_enable_vpngw     = bool<br>    is_single_natgw     = bool<br>    is_one_natgw_per_az = bool<br>    db_sub_grp_create   = bool<br>    db_sub_rt_create    = bool<br>  })</pre> | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| database\_connection\_endpoint | Database Connection Endpoint |
| database\_instance\_address | Database Instance Address |
| database\_password | Database Password |
| database\_username | Database Username |
| eks\_security\_group | EKS Security Group |
| kubeconfig | Kubeconfig Output |
| private\_key | Private Pem Key |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
