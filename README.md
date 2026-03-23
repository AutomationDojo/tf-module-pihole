# terraform-pihole-management

[![Registry](https://img.shields.io/badge/Terraform%20Registry-AutomationDojo%2Fmanagement%2Fpihole-purple)](https://registry.terraform.io/modules/AutomationDojo/management/pihole/latest)
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](LICENSE)

Terraform/OpenTofu modules for managing [Pi-hole v6](https://pi-hole.net/) as code using the [dklesev/pihole](https://registry.terraform.io/providers/dklesev/pihole/latest) provider.

📖 **[Full documentation](https://pihole-terraform-module.automationdojo.org)**

---

## Overview

This collection of modules covers the full Pi-hole configuration surface:

| Module | Description |
|--------|-------------|
| [groups](modules/groups/) | Manage Pi-hole groups for client segmentation |
| [dns](modules/dns/) | Upstream DNS servers, DNS settings, local A and CNAME records |
| [domains](modules/domains/) | Allow/deny domain entries (exact and regex) |
| [lists](modules/lists/) | Adlist and allowlist subscriptions |
| [dhcp](modules/dhcp/) | DHCP server settings and static leases |
| [privacy](modules/privacy/) | Privacy level and database retention settings |
| [webserver](modules/webserver/) | Web interface and API settings |

---

## Requirements

| Name | Version |
|------|---------|
| Terraform / OpenTofu | >= 1.0 |
| [dklesev/pihole](https://registry.terraform.io/providers/dklesev/pihole/latest) | ~> 1.0 |

> **Note:** This module requires Pi-hole v6 or later. The `dklesev/pihole` provider uses the Pi-hole v6 REST API, which is not compatible with Pi-hole v5.

---

## Provider Configuration

```hcl
terraform {
  required_providers {
    pihole = {
      source  = "dklesev/pihole"
      version = "~> 1.0"
    }
  }
}

provider "pihole" {
  url      = "https://pihole.example.com"
  password = var.pihole_password
}
```

---

## Usage

Each module can be used independently. Below is a complete example managing all aspects of a Pi-hole instance.

### Complete Example

```hcl
module "groups" {
  source  = "AutomationDojo/management/pihole//modules/groups"
  version = "1.0.3"

  groups = {
    Default = {
      enabled     = true
      description = "The default group"
    }
  }
}

module "dns" {
  source  = "AutomationDojo/management/pihole//modules/dns"
  version = "1.0.3"

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

module "domains" {
  source  = "AutomationDojo/management/pihole//modules/domains"
  version = "1.0.3"

  default_groups = [module.groups.group_ids["Default"]]

  domains = {
    block_ads = {
      domain  = "*.ads.example.com"
      type    = "deny"
      kind    = "regex"
      comment = "Block ads"
    }
  }
}

module "lists" {
  source  = "AutomationDojo/management/pihole//modules/lists"
  version = "1.0.3"

  default_groups = [module.groups.group_ids["Default"]]

  lists = {
    stevenblack = {
      address = "https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
      type    = "block"
      comment = "StevenBlack unified hosts"
    }
    hagezi_pro = {
      address = "https://raw.githubusercontent.com/hagezi/dns-blocklists/main/adblock/pro.txt"
      type    = "block"
      comment = "Hagezi Pro"
    }
  }
}

module "dhcp" {
  source  = "AutomationDojo/management/pihole//modules/dhcp"
  version = "1.0.3"

  dhcp_settings = {
    active = true
    start  = "192.168.1.2"
    end    = "192.168.1.254"
    router = "192.168.1.1"
    ipv6   = true
  }

  static_leases = {
    raspberry_pi = {
      mac      = "b8:27:eb:b8:66:83"
      ip       = "192.168.1.10"
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

---

## Importing Existing Pi-hole Configuration

If you already have a Pi-hole instance configured, you can import existing resources into Terraform state using import blocks. Each module's documentation covers the import format for its resources.

**Example — import the Default group:**

```hcl
import {
  to = module.groups.pihole_group.groups["Default"]
  id = "Default"
}
```

**Example — import an adlist:**

```hcl
import {
  to = module.lists.pihole_list.lists["stevenblack"]
  id = "block/https://raw.githubusercontent.com/StevenBlack/hosts/master/hosts"
}
```

See each submodule's documentation for full import reference.

---

## License

[Apache 2.0](LICENSE)
