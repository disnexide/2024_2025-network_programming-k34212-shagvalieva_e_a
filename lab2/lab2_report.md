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

Проверка локальной связности:
![image](https://github.com/user-attachments/assets/701b2ae3-edbc-4d88-a05d-e46a4ec5a014)
![image](https://github.com/user-attachments/assets/69accc23-a7f7-4a21-b2d6-39cfa6ce0e85)

3. Создание файла Inventory для Ansible
   Был составлен файл inventory.yml, который включает два устройства с соответствующими IP-адресами и данными для подключения:

![image](https://github.com/user-attachments/assets/956699b2-780b-495f-82a2-77d9b4f714de)





