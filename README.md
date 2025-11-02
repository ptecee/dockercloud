# Docker cloud

Данный код создает виртуальную машину c внешним ip в облаке Yandex Cloud. _В дальнейшем должна быть добавлена предустановка docker и golang._ 


## Файл `terraform.tfvars`
Перед созданием VM, необходимо создать файл `terrafrom.tfvars` с след. переменными:
```tf
yandex_token        = <yc iam create-token>
yandex_cloud_id     = <yc config get cloud-id>
yandex_folder_id    = <yc config get folder-id>
```

## Создание и удаление VM

Применить когнфигурацию Terraform
```shell
terrafrom init
terrafrom plan
terrafrom apply
```