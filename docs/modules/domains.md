# domains

Manages Pi-hole allow/deny domain entries (exact and regex).

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `default_groups` | `list(number)` | `[]` | Default group IDs to assign to all domains |
| `domains` | `map(object)` | `{}` | Map of domain entries |

### `domains` object

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `domain` | `string` | required | Domain name or regex pattern |
| `type` | `string` | required | `"allow"` or `"deny"` |
| `kind` | `string` | required | `"exact"` or `"regex"` |
| `enabled` | `bool` | `true` | Whether the entry is active |
| `comment` | `string` | `""` | Optional description |
| `groups` | `list(number)` | `null` | Override group IDs (uses `default_groups` if null) |

## Outputs

| Name | Description |
|------|-------------|
| `domains` | Map of domain entries created |

## Example

```hcl
module "domains" {
  source  = "AutomationDojo/management/pihole//modules/domains"
  version = "1.0.5"

  default_groups = [0]

  domains = {
    zscaler_com = {
      domain  = "*.zscaler.com"
      type    = "deny"
      kind    = "regex"
      comment = "Block Zscaler"
    }
    allow_example = {
      domain  = "example.com"
      type    = "allow"
      kind    = "exact"
    }
  }
}
```

## Import

Domains are imported using `type/kind/domain`:

```hcl
import {
  to = module.domains.pihole_domain.domains["zscaler_com"]
  id = "deny/regex/*.zscaler.com"
}
```
