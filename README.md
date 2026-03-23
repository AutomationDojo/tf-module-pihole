# terraform-pihole-management

Terraform/OpenTofu modules for managing Pi-hole v6 as code using the [dklesev/pihole](https://registry.terraform.io/providers/dklesev/pihole/latest) provider.

📖 **[Full documentation](https://pihole-terraform-module.automationdojo.org)**

## Modules

| Module | Description |
|--------|-------------|
| [groups](modules/groups/) | Manage Pi-hole groups |
| [dns](modules/dns/) | DNS settings, upstream servers, local A/CNAME records |
| [domains](modules/domains/) | Allow/deny domain entries (exact and regex) |
| [lists](modules/lists/) | Adlist and allowlist subscriptions |
| [dhcp](modules/dhcp/) | DHCP server settings and static leases |
| [privacy](modules/privacy/) | Privacy level and database settings |
| [webserver](modules/webserver/) | Web interface and API settings |

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

## Quick Start

```hcl
module "groups" {
  source  = "AutomationDojo/management/pihole//modules/groups"
  version = "1.0.3"

  groups = {
    Default = { enabled = true, description = "The default group" }
  }
}

module "dns" {
  source  = "AutomationDojo/management/pihole//modules/dns"
  version = "1.0.3"

  upstream_servers = ["8.8.8.8", "8.8.4.4", "1.1.1.1", "1.0.0.1"]

  dns_settings = {
    domain_name    = "lan"
    bogus_priv     = true
    listening_mode = "ALL"
  }
}

module "lists" {
  source  = "AutomationDojo/management/pihole//modules/lists"
  version = "1.0.3"

  default_groups = [0]

  lists = {
    stevenblack = {
      address = "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
      comment = "StevenBlack unified hosts"
    }
  }
}

module "dhcp" {
  source  = "AutomationDojo/management/pihole//modules/dhcp"
  version = "1.0.3"

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

module "privacy" {
  source  = "AutomationDojo/management/pihole//modules/privacy"
  version = "1.0.3"

  privacy_level  = 0
  max_db_days    = 91
  network_expire = 91
}

module "webserver" {
  source  = "AutomationDojo/management/pihole//modules/webserver"
  version = "1.0.3"

  interface_theme = "default-auto"
  interface_boxed = true
}
```

## License

Apache 2.0
