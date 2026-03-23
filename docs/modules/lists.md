# lists

Manages Pi-hole adlist and allowlist subscriptions.

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `default_groups` | `list(number)` | `[]` | Default group IDs to assign to all lists |
| `lists` | `map(object)` | `{}` | Map of subscription lists |

### `lists` object

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `address` | `string` | required | URL of the list |
| `type` | `string` | `"block"` | `"block"` or `"allow"` |
| `enabled` | `bool` | `true` | Whether the list is active |
| `comment` | `string` | `null` | Optional description |
| `groups` | `list(number)` | `null` | Override group IDs (uses `default_groups` if null) |

## Outputs

| Name | Description |
|------|-------------|
| `lists` | Map of subscription lists created |

## Example

```hcl
module "lists" {
  source  = "AutomationDojo/management/pihole//modules/lists"
  version = "1.0.6"

  default_groups = [0]

  lists = {
    stevenblack = {
      address = "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
      comment = "StevenBlack unified hosts"
    }
    hagezi_pro = {
      address = "https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt"
      comment = "Hagezi Pro"
    }
  }
}
```

## Import

Lists are imported using `type/address`:

```hcl
import {
  to = module.lists.pihole_list.lists["stevenblack"]
  id = "block/https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
}
```
