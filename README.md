# devops-netology
Выполнение домашеного задания №1

# Будет игнорировать все файлы в директории .terraform во всех встречающихся директориях
**/.terraform/*

# исключает все файлы с расширением .tfstate и .tfstate.*
*.tfstate
*.tfstate.*

# Исключает файл crush.log
crash.log

# исключает все файлы с расширением *.tfvars
*.tfvars

# Будут игнорироваться все файлы, в имени которых содержиться:  override.tf override.tf.json
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Будет игнорироваться .terraformrc terraform.rc
.terraformrc
terraform.rc
