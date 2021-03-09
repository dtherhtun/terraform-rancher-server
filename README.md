# Rancher Common Terraform Module

The `rancher-common` module contains all resources that do not depend on a
specific cloud provider. RKE, Kubernetes, Helm, and Rancher providers are used
given the necessary information about the infrastructure created in a cloud
provider.

## Variables

###### `node_public_ip`
- **Required**
Public IP of compute node for Rancher cluster

###### `node_internal_ip`
- Default: **`""`**
Internal IP of compute node for Rancher cluster

###### `node_username`
- **Required**
Username used for SSH access to the Rancher server cluster node

###### `ssh_private_key_pem`
- **Required**
Private key used for SSH access to the Rancher server cluster node

Expected to be in PEM format.

###### `rke_kubernetes_version`
- Default: **`"v1.19.4-rancher1-1"`**
Kubernetes version to use for Rancher server RKE cluster

###### `cert_manager_version`
- Default: **`"1.0.4"`**
Version of cert-manager to install alongside Rancher (format: `0.0.0`)

Available versions are found in `files/cert-manager`, where a supported version
is indicated by the presence of `crds-${var.cert_manager_version}.yaml`.

###### `rancher_version`
- Default: **`"v2.5.3"`**
Rancher server version (format `v0.0.0`)

###### `rancher_server_dns`
- **Required**
DNS host name of the Rancher server

A DNS name is required to allow successful SSL cert generation.
SSL certs may only be assigned to DNS names, not IP addresses.
Only an IP address could cause the Custom cluster to fail due to mismatching SSL
Subject Names.

###### `admin_password`
- **Required**
Admin password to use for Rancher server bootstrap

Log in to the Rancher server using username `admin` and this password.

###### `workload_kubernetes_version`
- Default: **`"v1.18.12-rancher1-1"`**
Kubernetes version to use for managed workload cluster

Defaulted to one version behind most recent minor release to allow experimenting
with upgrading Kubernetes versions.

###### `workload_cluster_name`
- **Required**
Name for created custom workload cluster


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
| helm | 1.3.2 |
| k8s | 0.8.2 |
| local | 2.0.0 |
| rancher2.admin | 1.10.6 |
| rancher2.bootstrap | 1.10.6 |
| rke | 1.1.6 |

## Modules

No Modules.

## Resources

| Name |
|------|
| [helm_release](https://registry.terraform.io/providers/hashicorp/helm/1.3.2/docs/resources/release) |
| [k8s_manifest](https://registry.terraform.io/providers/banzaicloud/k8s/0.8.2/docs/resources/manifest) |
| [local_file](https://registry.terraform.io/providers/hashicorp/local/2.0.0/docs/resources/file) |
| [rancher2_bootstrap](https://registry.terraform.io/providers/rancher/rancher2/1.10.6/docs/resources/bootstrap) |
| [rancher2_cluster](https://registry.terraform.io/providers/rancher/rancher2/1.10.6/docs/resources/cluster) |
| [rke_cluster](https://registry.terraform.io/providers/rancher/rke/1.1.6/docs/resources/cluster) |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| admin\_password | Admin password to use for Rancher server bootstrap | `string` | n/a | yes |
| cert\_manager\_version | Version of cert-manager to install alongside Rancher (format: 0.0.0) | `string` | `"1.0.4"` | no |
| node\_internal\_ip | Internal IP of compute node for Rancher cluster | `string` | `""` | no |
| node\_public\_ip | Public IP of compute node for Rancher cluster | `string` | n/a | yes |
| node\_username | Username used for SSH access to the Rancher server cluster node | `string` | n/a | yes |
| rancher\_server\_dns | DNS host name of the Rancher server | `string` | n/a | yes |
| rancher\_version | Rancher server version (format v0.0.0) | `string` | `"v2.5.3"` | no |
| rke\_kubernetes\_version | Kubernetes version to use for Rancher server RKE cluster | `string` | `"v1.19.4-rancher1-1"` | no |
| rke\_network\_options | Network options used for the custom workload cluster | `any` | `null` | no |
| rke\_network\_plugin | Network plugin used for the custom workload cluster | `string` | `"canal"` | no |
| ssh\_private\_key\_pem | Private key used for SSH access to the Rancher server cluster node | `string` | n/a | yes |
| windows\_prefered\_cluster | Activate windows supports for the custom workload cluster | `bool` | `false` | no |
| workload\_cluster\_name | Name for created custom workload cluster | `string` | n/a | yes |
| workload\_kubernetes\_version | Kubernetes version to use for managed workload cluster | `string` | `"v1.18.12-rancher1-1"` | no |

## Outputs

| Name | Description |
|------|-------------|
| custom\_cluster\_command | Docker command used to add a node to the quickstart cluster |
| custom\_cluster\_windows\_command | Docker command used to add a windows node to the quickstart cluster |
| rancher\_url | n/a |
<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
