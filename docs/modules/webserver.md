# webserver

Manages Pi-hole web interface and API settings.

!!! note
    Not all web interface settings are supported by the provider. Unsupported settings include: Prettify API output, Permit destructive actions, Exclusions, and 2FA.

## Variables

| Name | Type | Default | Description |
|------|------|---------|-------------|
| `interface_boxed` | `bool` | `true` | Use the boxed layout |
| `interface_theme` | `string` | `"default-auto"` | Web interface theme |
| `session_timeout` | `number` | `1800` | Session timeout in seconds |
| `session_restore` | `bool` | `true` | Restore sessions on FTL restart |
| `threads` | `number` | `50` | Number of webserver worker threads |

### Available themes

| Value | Description |
|-------|-------------|
| `default-auto` | Follow system preference |
| `default-light` | Light mode |
| `default-dark` | Dark mode |

## Outputs

| Name | Description |
|------|-------------|
| `interface_theme` | Configured web interface theme |
| `session_timeout` | Configured session timeout |

## Example

```hcl
module "webserver" {
  source = "github.com/AutomationDojo/tf-module-pihole//modules/webserver?ref=v1.0.1"

  interface_boxed = true
  interface_theme = "default-auto"
  session_timeout = 1800
  session_restore = true
  threads         = 50
}
```

## Import

```hcl
import {
  to = module.webserver.pihole_config_webserver.settings
  id = "webserver"
}
```
