# tf-module-pihole

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
      comment = "StevenBlack unified hosts"
    }
  }
}

module "dhcp" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/dhcp?ref=v1.0.1"

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
  source = "github.com/AutomationDojo/tf-module-pihole//modules/privacy?ref=v1.0.1"

  privacy_level  = 0
  max_db_days    = 91
  network_expire = 91
}

module "webserver" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/webserver?ref=v1.0.1"

  interface_theme = "default-auto"
  interface_boxed = true
}
```

## License

Apache 2.0
