# Cloud Function

## Description

The component provisions http triggered GCP Cloud Function with Node JS engine and helloworld example with help of terraform

## Structure

The component has the following directory structure:

```text
./
├── hub-component.yaml # manifest
├── main.tf            # terraform configuration
├── ouputs.tf          # terraform outputs
└── variables.tf       # terraform variables
```

## Parameters

| Name      | Description | Default Value | Required |
| :-------- | :--------   | :--------     | :--:     |
| `cloudFunction.name` | Name of Cloud Function |  | x |

## Outputs

| Name      | Description |
| :-------- | :--------   |
| `cloudFunction.url` | Cloud Function trigger url |

## References

* [Helloworld example](https://cloud.google.com/functions/docs/samples/functions-helloworld-get#functions_helloworld_get-nodejs)
* [Terraform provider Cloud Function resource](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/cloudfunctions_function)
