# dns

Manages Pi-hole DNS settings, upstream servers, and local DNS records (A and CNAME).

## Usage

```hcl
module "dns" {
  source  = "AutomationDojo/management/pihole//modules/dns"
  version = "1.0.6"

  upstream_servers = [
    "8.8.8.8",
    "8.8.4.4",
    "1.1.1.1",
    "1.0.0.1",
  ]

  dns_settings = {
    domain_name    = "lan"
    bogus_priv     = true
    listening_mode = "ALL"
  }

  a_records = {
    "nas.lan" = "192.168.1.10"
  }

  cname_records = {
    "media.lan" = "nas.lan"
  }
}
```

## Import

DNS configuration:

```hcl
import {
  to = module.dns.pihole_config_dns.settings[0]
  id = "dns"
}
```

Upstream servers (one block per server):

```hcl
import {
  to = module.dns.pihole_dns_upstream.upstream["8.8.8.8"]
  id = "8.8.8.8"
}
```

Local A records:

```hcl
import {
  to = module.dns.pihole_local_dns.a_records["nas.lan"]
  id = "nas.lan/192.168.1.10"
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
| <a name="input_a_records"></a> [a\_records](#input\_a\_records) | Map of local DNS A records (hostname -> IP) | `map(string)` | `{}` | no |
| <a name="input_cname_records"></a> [cname\_records](#input\_cname\_records) | Map of local DNS CNAME records (hostname -> target) | `map(string)` | `{}` | no |
| <a name="input_dns_settings"></a> [dns\_settings](#input\_dns\_settings) | Pi-hole DNS configuration settings | <pre>object({<br/>    dnssec              = optional(bool, false)<br/>    query_logging       = optional(bool, true)<br/>    blocking_active     = optional(bool, true)<br/>    blocking_mode       = optional(string, "NULL")<br/>    block_ttl           = optional(number, 2)<br/>    cache_size          = optional(number, 10000)<br/>    cache_optimizer     = optional(number, 3600)<br/>    rate_limit_count    = optional(number, 1000)<br/>    rate_limit_interval = optional(number, 60)<br/>    domain_name         = optional(string, "lan")<br/>    domain_local        = optional(bool, true)<br/>    domain_needed       = optional(bool, false)<br/>    bogus_priv          = optional(bool, true)<br/>    expand_hosts        = optional(bool, false)<br/>    listening_mode      = optional(string, "local")<br/>  })</pre> | `{}` | no |
| <a name="input_upstream_servers"></a> [upstream\_servers](#input\_upstream\_servers) | List of upstream DNS server IPs | `list(string)` | `[]` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_a_records"></a> [a\_records](#output\_a\_records) | Map of local DNS A records created |
| <a name="output_cname_records"></a> [cname\_records](#output\_cname\_records) | Map of CNAME records created |
<!-- END_TF_DOCS -->
