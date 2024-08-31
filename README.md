"# packer-learn" 






## Variable

### locals variable block

aws-build.pkr.hcl

```
locals {
  timestamp = regex_replace(timestamp(), "[- TZ:]", "")
}

```

### variable block

aws-build.pkr.hcl

```
variable "image_id" {
    type = string
    description = "value of string id"
    default = "ami-12345"
}
```


### variable file

variables.pkvars.hcl

```
image_id = "ami-12345"
```


### Environment Variable

```
export PKR_VAR_secret_key=secretkey
export PKR_VAR_access_key=accesskey

```

## Use Variable

