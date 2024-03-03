Домашнее задание к занятию «Введение в Terraform»
Задание 1
1) версия terraform

![image](https://github.com/ArtemDuke/ArtemDuke-shrdevops-4-terraform_homework_1/assets/161213872/3da00369-6451-4ba3-bcb9-ff90254eb664)

2) согласно этому .gitignore допустимо хранить в personal.auto.tfvars
3) "result": "XEUuuX4EcUWR5JqO"
4) не указан второй лейбл для первоо блока
во втором блоке название второго лейбла начинается с цифры, допустимы только буквы или _
5) иправленный код main.tf
```
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 9090
  }
}
```
![image](https://github.com/ArtemDuke/ArtemDuke-shrdevops-4-terraform_homework_1/assets/161213872/3a54d073-a422-4e37-ac5a-0e5995f5b359)
6) 
Применение ключа -autoapprve не требует ручного подтвержденяи изменений плана, удобно для автоматизированных сбороr ci/cd. Допустимо использовать при оранниченом числе пользователей с правами на редактирование плана. Это сводит к минимуму риск непредсказуемых изменений.
![image](https://github.com/ArtemDuke/ArtemDuke-shrdevops-4-terraform_homework_1/assets/161213872/e925b506-945a-4c61-a20b-ec2dbd2913ed)
7) содержимое .tfstate после удалёнеия

```
{
  "version": 4,
  "terraform_version": "1.7.4",
  "serial": 21,
  "lineage": "b5e2c80f-6328-3c62-f502-d4ebb2691f97",
  "outputs": {},
  "resources": [],
  "check_results": null
}
```

образ не был удалён, т.к. для keep_locally было устанвлено значение true

```
resource "docker_image" "nginx"_latest {
  name         = "nginx:latest"
  keep_locally = true
}
```

строчка из документации:
```
keep_locally (Boolean) If true, then the Docker image won't be deleted on destroy operation. If this is false, it will delete the image from the docker local storage on destroy operation.
```
