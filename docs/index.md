# tf-module-pihole

Terraform/OpenTofu modules for managing Pi-hole v6 as code using the [dklesev/pihole](https://registry.terraform.io/providers/dklesev/pihole/latest) provider.

[:fontawesome-brands-github: GitHub](https://github.com/AutomationDojo/tf-module-pihole){ .md-button }

## Modules

| Module | Description |
|--------|-------------|
| [groups](modules/groups.md) | Manage Pi-hole groups |
| [dns](modules/dns.md) | DNS settings, upstream servers, local A/CNAME records |
| [domains](modules/domains.md) | Allow/deny domain lists |
| [lists](modules/lists.md) | Adlist and allowlist subscriptions |
| [dhcp](modules/dhcp.md) | DHCP server settings and static leases |
| [privacy](modules/privacy.md) | Privacy level and database settings |
| [webserver](modules/webserver.md) | Web interface and API settings |

## Requirements

| Name | Version |
|------|---------|
| Terraform / OpenTofu | >= 1.0 |
| dklesev/pihole | ~> 1.0 |

## Provider Configuration

```hcl
provider "pihole" {
  url      = "https://pihole.example.com"
  password = var.pihole_password
}
```

## Example

```hcl
module "groups" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/groups?ref=v1.0.1"

  groups = {
    Default = { enabled = true, description = "The default group" }
  }
}

module "dns" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/dns?ref=v1.0.1"

  upstream_servers = ["8.8.8.8", "8.8.4.4", "1.1.1.1", "1.0.0.1"]

  dns_settings = {
    domain_name    = "lan"
    bogus_priv     = true
    listening_mode = "ALL"
  }
}

module "lists" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/lists?ref=v1.0.1"

  default_groups = [0]

  lists = {
    stevenblack = {
      address = "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
      type    = "block"
    }
  }
}
```
