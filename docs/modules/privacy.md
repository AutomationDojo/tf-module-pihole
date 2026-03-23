# privacy

Manages Pi-hole privacy level and database settings.

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `privacy_level` | `number` | `0` | Privacy level for statistics |
| `db_import` | `bool` | `true` | Import database on FTL startup |
| `max_db_days` | `number` | `365` | Max days to keep queries in the database |
| `network_expire` | `number` | `365` | Days to keep IPs in the network_addresses table |
| `etc_dnsmasq_d` | `bool` | `false` | Load config files from `/etc/dnsmasq.d` |

### Privacy levels

| Value | Description |
|-------|-------------|
| `0` | Show everything and record everything |
| `1` | Hide domains — display and store all domains as `hidden` |
| `2` | Hide domains and clients |
| `3` | Anonymous mode — disables all statistics |

## Outputs

| Name | Description |
|------|-------------|
| `privacy_level` | Configured privacy level |
| `max_db_days` | Configured max DB days |

## Example

```hcl
module "privacy" {
  source = "github.com/AutomationDojo/terraform-pihole-management//modules/privacy?ref=v1.0.3"

  privacy_level  = 0
  db_import      = true
  max_db_days    = 91
  network_expire = 91
  etc_dnsmasq_d  = true
}
```

## Import

```hcl
import {
  to = module.privacy.pihole_config_misc.settings
  id = "misc"
}

import {
  to = module.privacy.pihole_config_database.settings
  id = "database"
}
```
