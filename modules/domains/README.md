# domains

Manages Pi-hole allow/deny domain entries (exact and regex).

## Usage

```hcl
module "domains" {
  source  = "AutomationDojo/management/pihole//modules/domains"
  version = "1.0.6"

  default_groups = [0]

  domains = {
    block_ads = {
      domain  = "ads.example.com"
      type    = "deny"
      kind    = "exact"
      comment = "Block ads domain"
    }
    block_trackers_regex = {
      domain  = "*.tracker.com"
      type    = "deny"
      kind    = "regex"
      comment = "Block tracker subdomains"
    }
    allow_safe = {
      domain  = "safe.example.com"
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
  to = module.domains.pihole_domain.domains["block_ads"]
  id = "deny/exact/ads.example.com"
}

import {
  to = module.domains.pihole_domain.domains["block_trackers_regex"]
  id = "deny/regex/*.tracker.com"
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
| <a name="input_default_groups"></a> [default\_groups](#input\_default\_groups) | Default group IDs to assign to all domains (can be overridden per domain) | `list(number)` | `[]` | no |
| <a name="input_domains"></a> [domains](#input\_domains) | Map of domain entries for allow/deny lists | <pre>map(object({<br/>    domain  = string<br/>    type    = string<br/>    kind    = string<br/>    enabled = optional(bool, true)<br/>    comment = optional(string, "")<br/>    groups  = optional(list(number), null)<br/>  }))</pre> | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_domains"></a> [domains](#output\_domains) | Map of domain entries created |
<!-- END_TF_DOCS -->
