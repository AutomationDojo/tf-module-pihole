# tf-module-pihole

OpenTofu/Terraform modules for managing Pi-hole v6 as code using the [dklesev/pihole](https://registry.terraform.io/providers/dklesev/pihole/latest) provider.

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
| OpenTofu | >= 1.0 |
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
  source = "path/to/modules/groups"

  groups = {
    Default = { enabled = true, description = "The default group" }
  }
}

module "dns" {
  source = "path/to/modules/dns"

  upstream_servers = ["8.8.8.8", "8.8.4.4", "1.1.1.1", "1.0.0.1"]

  dns_settings = {
    domain_name    = "lan"
    bogus_priv     = true
    listening_mode = "ALL"
  }
}

module "lists" {
  source = "path/to/modules/lists"

  default_groups = [0]

  lists = {
    stevenblack = {
      address = "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
      comment = "StevenBlack unified hosts"
    }
  }
}

module "dhcp" {
  source = "path/to/modules/dhcp"

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
  source = "path/to/modules/privacy"

  privacy_level  = 0
  max_db_days    = 91
  network_expire = 91
}

module "webserver" {
  source = "path/to/modules/webserver"

  interface_theme = "default-auto"
  interface_boxed = true
}
```

## License

Apache 2.0
