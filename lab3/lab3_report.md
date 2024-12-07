University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)

Year: 2024/2025

Group: K34212

Author: Shagvalieva Ekaterina Albertovna

Lab: Lab3

Date of create: 05-Nov 2024

Date of finished: 

# Лабораторная работ №3 "Развертывание Netbox, сеть связи как источник правды в системе технического учета Netbox"

## Цель работы

С помощью Ansible и Netbox собрать всю возможную информацию об устройствах и сохранить их в отдельном файле.

## Ход работы


Для начала на новую виртуальную машину был установлен Netbox.

![image](https://github.com/user-attachments/assets/a3edfaf2-fb4a-43b5-bc88-6527e35fdb76)

После успешного создания и активации виртуального окружения, а также установки всех зависимостей Netbox, можно продолжить с настройкой и запуском Netbox.
Создадим БД и пользователя в ней.

![image](https://github.com/user-attachments/assets/b545cae0-8361-465e-93e2-cf4f579dba9f)


![image](https://github.com/user-attachments/assets/184cc4b9-6463-4ce3-a2bc-ba4f0dce20b9)

И завершим настройку запуском.

![image](https://github.com/user-attachments/assets/16338a1d-3ab5-4da4-9622-3ccd68268712)

Теперь появилась возможность зайти в Netbox. Там добавляем наши устройства.

![image](https://github.com/user-attachments/assets/d6888e03-19c1-43ac-b4cb-5281a8b9ebd6)

Затем 

```
plugin: netbox.netbox.nb_inventory
api_endpoint: http://130.193.42.42:8080/
token: "токен"
validate_certs: False
config_context: False
interfaces: True
```

```
ansible-inventory -v --list -y -i netbox_inventory.yml > nb_inventory.yml
```
