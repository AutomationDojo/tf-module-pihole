# dns

Manages Pi-hole DNS settings, upstream servers, and local DNS records (A and CNAME).

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `upstream_servers` | `list(string)` | `[]` | List of upstream DNS server IPs |
| `dns_settings` | `object` | `{}` | Pi-hole DNS configuration settings |
| `a_records` | `map(string)` | `{}` | Local DNS A records (hostname → IP) |
| `cname_records` | `map(string)` | `{}` | Local DNS CNAME records (hostname → target) |

### `dns_settings` object

| Attribute | Type | Default | Description |
|-----------|------|---------|-------------|
| `dnssec` | `bool` | `false` | Enable DNSSEC validation |
| `query_logging` | `bool` | `true` | Log DNS queries and replies |
| `blocking_active` | `bool` | `true` | Enable Pi-hole blocking |
| `blocking_mode` | `string` | `"NULL"` | Blocking mode (`NULL`, `IP`, `NXDOMAIN`, etc.) |
| `block_ttl` | `number` | `2` | TTL for blocked responses |
| `cache_size` | `number` | `10000` | DNS cache size |
| `cache_optimizer` | `number` | `3600` | Cache optimizer interval (seconds) |
| `rate_limit_count` | `number` | `1000` | Rate limit query count |
| `rate_limit_interval` | `number` | `60` | Rate limit interval (seconds) |
| `domain_name` | `string` | `"lan"` | Local domain name |
| `domain_local` | `bool` | `true` | Treat domain as local only |
| `domain_needed` | `bool` | `false` | Never forward non-FQDN queries |
| `bogus_priv` | `bool` | `true` | Never forward reverse lookups for private IP ranges |
| `expand_hosts` | `bool` | `false` | Expand hostnames with domain suffix |
| `listening_mode` | `string` | `"local"` | Interface listening mode (`local`, `ALL`, etc.) |

## Outputs

| Name | Description |
|------|-------------|
| `a_records` | Map of local DNS A records created |
| `cname_records` | Map of CNAME records created |

## Example

```hcl
module "dns" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/dns?ref=v1.0.1"

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

DNS config:

```hcl
import {
  to = module.dns.pihole_config_dns.settings[0]
  id = "dns"
}
```

Upstream servers (one per server):

```hcl
import {
  to = module.dns.pihole_dns_upstream.upstream["8.8.8.8"]
  id = "8.8.8.8"
}
```
