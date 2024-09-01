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

```
ami_name      = "${var.ami_prefix}-${local.timestamp}"
```

using local
```
ami_name      = "ami-12345-{{local.timestamp}}"
```

calling variable
```
ami_name = var.ami_name
```

interpolate variable with strings
```
ami_name      = "${var.ami_prefix}-aws"
```

Build the image with the --var-file flag.

```
packer build --var-file=variables.pkrvars.hcl aws-ubuntu.pkr.hcl
```

Packer will automatically load any variable file that matches the name *.auto.pkrvars.hcl, without the need to pass the file via the command line.

Rename your variable file so Packer automatically loads it.

```
mv variables.pkrvars.hcl variables.auto.pkrvars.hcl
```


## Provisioner

upload single file

```
provisioner "file" {
    source = "packer.zip"
    destination = "/tmp/packer.zip"
}
```

upload multiple files

```
provisioner "file" {
    source = "/files"
    destination = "/tmp"
}
```

execute a script

```
provisioner "shell" {
    script = "install.sh"
}
```

run a command on the machine
```
provisioner "shell" {
    inline = [
        "echo "Installing updates",
        "sudo apt update",
        "sudo apt install nginx -y"
    ]
}
```

run a powershell script

```
provisioner "powershell" {
    script = [".scripts/win2019.ps1"]
}
```

