# Cloud Lab

This terraform configuration create a virtual machine with external ip addres in Yandex Cloud infrastracture.


## File `terraform.tfvars`
Before creating VM, you need create a `terraform.tfvars` file with the following variables (`yc` commands imply that you have perviously installed Yandex CLI):
```tf
yandex_token        = <yc iam create-token>
yandex_cloud_id     = <yc config get cloud-id>
yandex_folder_id    = <yc config get folder-id>
```

## Creating and removing VM

Apply Terraform configuration:
```shell
terrafrom init
terrafrom plan
terrafrom apply
```

Destroy resources:
```shell
terraform destroy
```

## Resources
By default, it is set `cpu = 2` and `ram = 4`. It's defined in `terraform.tfvars`.  
You can set other vars during the `terraform.tfvars` execution with:  

```shell
# Pass specific vars or...
terraform apply \
-var="def_numbers_of_cores=8" \
-var="def_ram_size=16"

# pass the file with vars
terraform apply \
-var-file="dev.tfvars"
```


## Problems that may arise

If you see errors like this in file `/var/log/cloud-init-output.log` while applying `cloud-init` file:
If you see errors like...
```
2025-11-08 10:01:59,480 - __init__.py[WARNING]: Unhandled non-multipart (text/x-not-multipart) userdata: 'b'# cloud-config\\r'...'
```
`# cloud-config\\r` - it means that in the file use Windows-style line wrapping (CRLF instead of LF).  

You can fix this whith command:
```shell
sed -i 's/\r$//' scripts/cloud-init.yaml
```
> [!warning] You need execute this command before applying configuration. 
