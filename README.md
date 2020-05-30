# terraform-aws-efs

Terraform module to provision an AWS [`EFS`](https://aws.amazon.com/efs/) Network File System.

## Usage


**IMPORTANT:** The `master` branch is used in `source` just as an example. In your code, do not pin to `master` because there may be breaking changes between releases.
Instead pin to the release tag (e.g. `?ref=tags/x.y.z`) of one of our [latest releases](https://github.com/ceibo-it/terraform-aws-efs/releases).


Include this repository as a module in your existing terraform code:

```hcl
module "efs" {
  source     = "git::https://github.com/ceibo-it/terraform-aws-efs.git?ref=master"

  namespace          = "eg"
  stage              = "test"
  name               = "app"
  region             = "us-west-1"
  vpc_id             = var.vpc_id
  subnets            = var.private_subnets
  security_groups    = [var.security_group_id]
  zone_id            = var.aws_route53_dns_zone_id
}
```

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| attributes | Additional attributes (e.g. `1`) | list(string) | `<list>` | no |
| delimiter | Delimiter to be used between `namespace`, `environment`, `stage`, `name` and `attributes` | string | `-` | no |
| dns_name | Name of the CNAME record to create | string | `` | no |
| enabled | Set to false to prevent the module from creating any resources | bool | `true` | no |
| encrypted | If true, the file system will be encrypted | bool | `false` | no |
| environment | Environment, e.g. 'prod', 'staging', 'dev', 'pre-prod', 'UAT' | string | `` | no |
| kms_key_id | If set, use a specific KMS key | string | `null` | no |
| mount_target_ip_address | The address (within the address range of the specified subnet) at which the file system may be mounted via the mount target | string | `` | no |
| name | Solution name, e.g. 'app' or 'jenkins' | string | `` | no |
| namespace | Namespace, which could be your organization name or abbreviation, e.g. 'eg' or 'cp' | string | `` | no |
| performance_mode | The file system performance mode. Can be either `generalPurpose` or `maxIO` | string | `generalPurpose` | no |
| provisioned_throughput_in_mibps | The throughput, measured in MiB/s, that you want to provision for the file system. Only applicable with `throughput_mode` set to provisioned | string | `0` | no |
| region | AWS Region | string | - | yes |
| security_groups | Security group IDs to allow access to the EFS | list(string) | - | yes |
| stage | Stage, e.g. 'prod', 'staging', 'dev', OR 'source', 'build', 'test', 'deploy', 'release' | string | `` | no |
| subnets | Subnet IDs | list(string) | - | yes |
| tags | Additional tags (e.g. `map('BusinessUnit','XYZ')` | map(string) | `<map>` | no |
| throughput_mode | Throughput mode for the file system. Defaults to bursting. Valid values: `bursting`, `provisioned`. When using `provisioned`, also set `provisioned_throughput_in_mibps` | string | `bursting` | no |
| transition_to_ia | Indicates how long it takes to transition files to the IA storage class. Valid values: AFTER_7_DAYS, AFTER_14_DAYS, AFTER_30_DAYS, AFTER_60_DAYS and AFTER_90_DAYS | string | `` | no |
| vpc_id | VPC ID | string | - | yes |
| zone_id | Route53 DNS zone ID | string | `` | no |

## Outputs

| Name | Description |
|------|-------------|
| arn | EFS ARN |
| dns_name | EFS DNS name |
| host | Route53 DNS hostname for the EFS |
| id | EFS ID |
| mount_target_dns_names | List of EFS mount target DNS names |
| mount_target_ids | List of EFS mount target IDs (one per Availability Zone) |
| mount_target_ips | List of EFS mount target IPs (one per Availability Zone) |
| network_interface_ids | List of mount target network interface IDs |
| security_group_arn | EFS Security Group ARN |
| security_group_id | EFS Security Group ID |
| security_group_name | EFS Security Group name |

## Copyright

Copyright © 2020 [Ceibo IT](https://ceibo.it/copyright)


## License 

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0) 

See [LICENSE](LICENSE) for full details.

    Licensed to the Apache Software Foundation (ASF) under one
    or more contributor license agreements.  See the NOTICE file
    distributed with this work for additional information
    regarding copyright ownership.  The ASF licenses this file
    to you under the Apache License, Version 2.0 (the
    "License"); you may not use this file except in compliance
    with the License.  You may obtain a copy of the License at

      https://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing,
    software distributed under the License is distributed on an
    "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY
    KIND, either express or implied.  See the License for the
    specific language governing permissions and limitations
    under the License.


## NOTICE

terraform-aws-efs
Copyright 2020 Ceibo


This product includes software developed by
Cloud Posse, LLC (c) (https://cloudposse.com/)
Licensed under Apache License, Version 2.0
Copyright © 2017-2019 Cloud Posse, LLC