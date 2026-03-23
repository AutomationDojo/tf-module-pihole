<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.0 |
| <a name="requirement_pihole"></a> [pihole](#requirement\_pihole) | ~> 1.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_pihole"></a> [pihole](#provider\_pihole) | ~> 1.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_dhcp_settings"></a> [dhcp\_settings](#input\_dhcp\_settings) | Pi-hole DHCP server configuration | <pre>object({<br/>    active                  = optional(bool, false)<br/>    start                   = optional(string, "")<br/>    end                     = optional(string, "")<br/>    router                  = optional(string, "")<br/>    netmask                 = optional(string, "")<br/>    lease_time              = optional(string, "")<br/>    ipv6                    = optional(bool, false)<br/>    rapid_commit            = optional(bool, false)<br/>    ignore_unknown_clients  = optional(bool, false)<br/>    logging                 = optional(bool, false)<br/>    multi_dns               = optional(bool, false)<br/>  })</pre> | `{}` | no |
| <a name="input_static_leases"></a> [static\_leases](#input\_static\_leases) | Map of DHCP static leases (name -> mac/ip/hostname) | <pre>map(object({<br/>    mac      = string<br/>    ip       = string<br/>    hostname = optional(string, null)<br/>  }))</pre> | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_static_leases"></a> [static\_leases](#output\_static\_leases) | Map of static DHCP leases created |
<!-- END_TF_DOCS -->