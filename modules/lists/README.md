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
| <a name="input_default_groups"></a> [default\_groups](#input\_default\_groups) | Default group IDs to assign to all lists (can be overridden per list) | `list(number)` | `[]` | no |
| <a name="input_lists"></a> [lists](#input\_lists) | Map of subscription lists (adlists / allowlists) to manage | <pre>map(object({<br/>    address = string<br/>    type    = optional(string, "block") # "block" or "allow"<br/>    enabled = optional(bool, true)<br/>    comment = optional(string, null)<br/>    groups  = optional(list(number), null)<br/>  }))</pre> | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_lists"></a> [lists](#output\_lists) | Map of subscription lists created |
<!-- END_TF_DOCS -->