# dhcp

Manages Pi-hole DHCP server settings and static leases.

## Usage

```hcl
module "dhcp" {
  source  = "AutomationDojo/management/pihole//modules/dhcp"
  version = "1.0.6"

  dhcp_settings = {
    active = true
    start  = "192.168.1.2"
    end    = "192.168.1.254"
    router = "192.168.1.1"
    ipv6   = true
  }

  static_leases = {
    raspberry_pi = {
      mac      = "88:f5:a3:02:2d:a3"
      ip       = "192.168.1.10"
      hostname = "rasp"
    }
    nas = {
      mac      = "aa:bb:cc:dd:ee:ff"
      ip       = "192.168.1.20"
      hostname = "nas"
    }
  }
}
```

## Import

DHCP configuration:

```hcl
import {
  to = module.dhcp.pihole_config_dhcp.settings[0]
  id = "dhcp"
}
```

Static leases are imported using `MAC,IP,hostname`:

```hcl
import {
  to = module.dhcp.pihole_dhcp_static_lease.leases["raspberry_pi"]
  id = "88:f5:a3:02:2d:a3,192.168.1.10,rasp"
}
```

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
| <a name="input_dhcp_settings"></a> [dhcp\_settings](#input\_dhcp\_settings) | Pi-hole DHCP server configuration | <pre>object({<br/>    active                 = optional(bool, false)<br/>    start                  = optional(string, "")<br/>    end                    = optional(string, "")<br/>    router                 = optional(string, "")<br/>    netmask                = optional(string, "")<br/>    lease_time             = optional(string, "")<br/>    ipv6                   = optional(bool, false)<br/>    rapid_commit           = optional(bool, false)<br/>    ignore_unknown_clients = optional(bool, false)<br/>    logging                = optional(bool, false)<br/>    multi_dns              = optional(bool, false)<br/>  })</pre> | `{}` | no |
| <a name="input_static_leases"></a> [static\_leases](#input\_static\_leases) | Map of DHCP static leases (name -> mac/ip/hostname) | <pre>map(object({<br/>    mac      = string<br/>    ip       = string<br/>    hostname = optional(string, null)<br/>  }))</pre> | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_static_leases"></a> [static\_leases](#output\_static\_leases) | Map of static DHCP leases created |
<!-- END_TF_DOCS -->
