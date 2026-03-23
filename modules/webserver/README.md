# webserver

Manages Pi-hole web interface and API settings.

## Usage

```hcl
module "webserver" {
  source  = "AutomationDojo/management/pihole//modules/webserver"
  version = "1.0.4"

  interface_theme = "default-auto"
  interface_boxed = true
  session_timeout = 1800
}
```

### Available themes

| Value | Description |
|-------|-------------|
| `"default-auto"` | Follow system light/dark preference |
| `"default-light"` | Light theme |
| `"default-dark"` | Dark theme |

## Import

```hcl
import {
  to = module.webserver.pihole_config_webserver.settings
  id = "webserver"
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
| <a name="input_interface_boxed"></a> [interface\_boxed](#input\_interface\_boxed) | Use the boxed layout in the web interface | `bool` | `true` | no |
| <a name="input_interface_theme"></a> [interface\_theme](#input\_interface\_theme) | Theme for the web interface (e.g. 'default-auto', 'default-light', 'default-dark') | `string` | `"default-auto"` | no |
| <a name="input_session_restore"></a> [session\_restore](#input\_session\_restore) | Restore sessions on FTL restart | `bool` | `true` | no |
| <a name="input_session_timeout"></a> [session\_timeout](#input\_session\_timeout) | Session timeout in seconds | `number` | `1800` | no |
| <a name="input_threads"></a> [threads](#input\_threads) | Number of webserver worker threads | `number` | `50` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_interface_theme"></a> [interface\_theme](#output\_interface\_theme) | Configured web interface theme |
| <a name="output_session_timeout"></a> [session\_timeout](#output\_session\_timeout) | Configured session timeout |
<!-- END_TF_DOCS -->
