# dhcp

Manages Pi-hole DHCP server settings and static leases.

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `dhcp_settings` | `object` | `{}` | DHCP server configuration |
| `static_leases` | `map(object)` | `{}` | Map of static DHCP leases |

### `dhcp_settings` object

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `active` | `bool` | `false` | Enable DHCP server |
| `start` | `string` | `""` | Start of IP range |
| `end` | `string` | `""` | End of IP range |
| `router` | `string` | `""` | Gateway IP address |
| `netmask` | `string` | `""` | Subnet mask (empty = auto) |
| `lease_time` | `string` | `""` | Lease duration (e.g. `"24h"`, `"infinite"`) |
| `ipv6` | `bool` | `false` | Enable IPv6 support (SLAAC + RA) |
| `rapid_commit` | `bool` | `false` | Enable DHCPv4 rapid commit |
| `ignore_unknown_clients` | `bool` | `false` | Ignore clients not in static leases |
| `logging` | `bool` | `false` | Enable DHCP logging |
| `multi_dns` | `bool` | `false` | Advertise DNS server multiple times |

### `static_leases` object

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `mac` | `string` | required | MAC address of the device |
| `ip` | `string` | required | Reserved IP address |
| `hostname` | `string` | `null` | Optional hostname |

## Outputs

| Name | Description |
|------|-------------|
| `static_leases` | Map of static DHCP leases created |

## Example

```hcl
module "dhcp" {
<<<<<<< HEAD
  source  = "AutomationDojo/management/pihole//modules/dhcp"
  version = "1.0.4"
=======
  source = "github.com/AutomationDojo/terraform-pihole-management//modules/dhcp?ref=v1.0.3"
>>>>>>> 743cf3ecb8b9be637178ea90767d8fe37cf58760

  dhcp_settings = {
    active  = true
    start   = "192.168.1.2"
    end     = "192.168.1.254"
    router  = "192.168.1.1"
    ipv6    = true
  }

  static_leases = {
    rasp = {
      mac      = "b8:27:eb:b8:66:83"
      ip       = "192.168.1.210"
      hostname = "rasp"
    }
  }
}
```

## Import

DHCP config:

```hcl
import {
  to = module.dhcp.pihole_config_dhcp.settings[0]
  id = "dhcp"
}
```

Static leases use the format `MAC,IP,hostname`:

```hcl
import {
  to = module.dhcp.pihole_dhcp_static_lease.leases["rasp"]
  id = "b8:27:eb:b8:66:83,192.168.1.210,rasp"
}
```
