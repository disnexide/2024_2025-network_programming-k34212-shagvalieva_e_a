University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)

Year: 2024/2025

Group: K34212

Author: Shagvalieva Ekaterina Albertovna

Lab: Lab2

Date of create: 16-Oct 2024

Date of finished: 

# Лабораторная работa №2 "Развертывание дополнительного CHR, первый сценарий Ansible"

## Цель работы

С помощью Ansible настроить несколько сетевых устройств и собрать информацию о них. Правильно собрать файл Inventory.

## Ход работы

1. Установка второго CHR на ПК
   Был установлен второй CHR на локальной машине, использовав образ RouterOS и VirtualBox для виртуализации. Оба устройства были сконфигурированы с IP-адресами:
   CHR1: 192.168.0.123
   CHR2: 192.168.0.129

![image](https://github.com/user-attachments/assets/e997fc82-173e-4e4f-8161-98fb2ab0b3fb)

2. Организация второго OVPN-клиента на втором CHR
   Настроен второй OpenVPN клиент на CHR2 для обеспечения связи через VPN туннель. Использовались стандартные команды для настройки интерфейса и подключения к серверу. 

Файл конфигурации для соединения на интерфейсе:

![image](https://github.com/user-attachments/assets/e26415f0-4b52-4e9d-a354-ef10135af657)


3. Создание файла Inventory для Ansible
   Был составлен файл inventory.yml, который включает два устройства с соответствующими IP-адресами и данными для подключения:

```
all:
  hosts:
    CHR1:
      ansible_host: 192.168.0.123
      ansible_user: admin
      ansible_password: 1111
      ansible_connection: ssh
      ansible_ssh_common_args: '-o StrictHostKeyChecking=no'
    CHR2:
      ansible_host: 192.168.0.129
      ansible_user: admin
      ansible_password: 222
      ansible_connection: ssh
      ansible_ssh_common_args: '-o StrictHostKeyChecking=no'
```

4. Настройка логина и пароля на обоих CHR с помощью Ansible
   Для изменения пользовательских данных на обоих CHR был написан playbook Ansible:

```
- hosts: all
  tasks:
    - name: Change user password on RouterOS (CHR)
      community.routeros.command:
        commands:
          - /user set name=admin password=newpassword
```

5. Настройка NTP-клиента
   Был настроен NTP-клиент на обоих CHR, чтобы обеспечить синхронизацию времени с внешними серверами времени. Использовался Ansible playbook для внесения изменений на устройства:

```
- hosts: all
  tasks:
    - name: Set NTP client
      community.routeros.command:
        commands:
          - /system ntp client set enabled=yes primary-ntp=91.206.8.50 secondary-ntp=193.204.114.232
```

6. Настройка OSPF с указанием Router ID
   OSPF (Open Shortest Path First) был настроен для обоих роутеров, с уникальными Router ID для каждого устройства:
   CHR1: Router ID = 1.1.1.1
   CHR2: Router ID = 2.2.2.2

   Были добавлены сети для анонсирования через OSPF, и OSPF был активирован на интерфейсах.

```
- hosts: all
  tasks:
    - name: Set OSPF Router ID
      community.routeros.command:
        commands:
          - /routing ospf instance set default router-id=1.1.1.1
          - /routing ospf network add network=192.168.0.0/24 area=backbone
```

7. Сбор данных по топологии OSPF
   Используя модуль routeros_facts и routeros_command, были собраны данные о OSPF топологии, а также полная конфигурация устройства.

   В конечном итоге плейбук выглядит следующим образом:
   
![image](https://github.com/user-attachments/assets/956699b2-780b-495f-82a2-77d9b4f714de)

Проверка локальной связности:

![image](https://github.com/user-attachments/assets/701b2ae3-edbc-4d88-a05d-e46a4ec5a014)

![image](https://github.com/user-attachments/assets/69accc23-a7f7-4a21-b2d6-39cfa6ce0e85)

Схема связи:



## Вывод: 
Лабораторная работа продемонстрировала возможность автоматизации конфигурации сетевых устройств с использованием Ansible. Все поставленные задачи выполнены, включая настройку логина/пароля, синхронизацию времени через NTP, настройку OSPF и сбор данных о топологии сети.



