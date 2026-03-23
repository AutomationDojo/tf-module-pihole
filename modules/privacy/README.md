# privacy

Manages Pi-hole privacy level and database retention settings.

## Usage

```hcl
module "privacy" {
  source  = "AutomationDojo/management/pihole//modules/privacy"
  version = "1.0.6"

  privacy_level  = 0
  max_db_days    = 91
  network_expire = 91
}
```

### Privacy levels

| Level | Description |
|-------|-------------|
| `0` | Show everything and record everything |
| `1` | Hide domains — display and store all domains as `hidden` |
| `2` | Hide domains and clients |
| `3` | Anonymous mode — no history saved, no top lists |

## Import

```hcl
import {
  to = module.privacy.pihole_config_database.settings
  id = "database"
}

import {
  to = module.privacy.pihole_config_misc.settings
  id = "misc"
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
| <a name="input_db_import"></a> [db\_import](#input\_db\_import) | Import database on FTL startup | `bool` | `true` | no |
| <a name="input_etc_dnsmasq_d"></a> [etc\_dnsmasq\_d](#input\_etc\_dnsmasq\_d) | Load configuration files from /etc/dnsmasq.d | `bool` | `false` | no |
| <a name="input_max_db_days"></a> [max\_db\_days](#input\_max\_db\_days) | Maximum number of days to keep queries in the database | `number` | `365` | no |
| <a name="input_network_expire"></a> [network\_expire](#input\_network\_expire) | How long to keep IP addresses in the network\_addresses table (days) | `number` | `365` | no |
| <a name="input_privacy_level"></a> [privacy\_level](#input\_privacy\_level) | Privacy level for statistics (0=show everything, 1=hide domains, 2=hide domains and clients, 3=anonymous mode) | `number` | `0` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_max_db_days"></a> [max\_db\_days](#output\_max\_db\_days) | Configured max DB days |
| <a name="output_privacy_level"></a> [privacy\_level](#output\_privacy\_level) | Configured privacy level |
<!-- END_TF_DOCS -->
