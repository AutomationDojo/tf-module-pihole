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
| <a name="input_groups"></a> [groups](#input\_groups) | Map of Pi-hole groups to create | <pre>map(object({<br/>    enabled     = optional(bool, true)<br/>    description = optional(string, "")<br/>  }))</pre> | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_group_ids"></a> [group\_ids](#output\_group\_ids) | Map of group name -> ID, useful for referencing in other modules |
| <a name="output_groups"></a> [groups](#output\_groups) | Map of groups created, including their IDs |
<!-- END_TF_DOCS -->