# groups

Manages Pi-hole groups. Groups allow you to apply different blocking rules to sets of clients.

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `groups` | `map(object)` | `{}` | Map of groups to create |

### `groups` object

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `enabled` | `bool` | `true` | Whether the group is active |
| `description` | `string` | `""` | Group description |

## Outputs

| Name | Description |
|------|-------------|
| `groups` | Map of groups created, including their IDs |
| `group_ids` | Map of group name → ID, useful for referencing in other modules |

## Example

```hcl
module "groups" {
<<<<<<< HEAD
  source  = "AutomationDojo/management/pihole//modules/groups"
  version = "1.0.4"
=======
  source = "github.com/AutomationDojo/terraform-pihole-management//modules/groups?ref=v1.0.3"
>>>>>>> 743cf3ecb8b9be637178ea90767d8fe37cf58760

  groups = {
    Default = {
      enabled     = true
      description = "The default group"
    }
    kids = {
      enabled     = true
      description = "Children devices"
    }
  }
}
```

## Import

Groups are imported by name:

```hcl
import {
  to = module.groups.pihole_group.groups["Default"]
  id = "Default"
}
```
