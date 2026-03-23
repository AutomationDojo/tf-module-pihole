# terraform-pihole-management

Terraform/OpenTofu modules for managing Pi-hole v6 as code using the [dklesev/pihole](https://registry.terraform.io/providers/dklesev/pihole/latest) provider.

[:fontawesome-brands-github: GitHub](https://github.com/AutomationDojo/terraform-pihole-management){ .md-button }

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
<<<<<<< HEAD
  source  = "AutomationDojo/management/pihole//modules/groups"
  version = "1.0.4"
=======
  source = "github.com/AutomationDojo/terraform-pihole-management//modules/groups?ref=v1.0.3"
>>>>>>> 743cf3ecb8b9be637178ea90767d8fe37cf58760

  groups = {
    Default = { enabled = true, description = "The default group" }
  }
}

module "dns" {
<<<<<<< HEAD
  source  = "AutomationDojo/management/pihole//modules/dns"
  version = "1.0.4"
=======
  source = "github.com/AutomationDojo/terraform-pihole-management//modules/dns?ref=v1.0.3"
>>>>>>> 743cf3ecb8b9be637178ea90767d8fe37cf58760

  upstream_servers = ["8.8.8.8", "8.8.4.4", "1.1.1.1", "1.0.0.1"]

  dns_settings = {
    domain_name    = "lan"
    bogus_priv     = true
    listening_mode = "ALL"
  }
}

module "lists" {
<<<<<<< HEAD
  source  = "AutomationDojo/management/pihole//modules/lists"
  version = "1.0.4"
=======
  source = "github.com/AutomationDojo/terraform-pihole-management//modules/lists?ref=v1.0.3"
>>>>>>> 743cf3ecb8b9be637178ea90767d8fe37cf58760

  default_groups = [0]

  lists = {
    stevenblack = {
      address = "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
      type    = "block"
    }
  }
}
```
