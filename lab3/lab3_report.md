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

[![image](https://github.com/user-attachments/assets/a3edfaf2-fb4a-43b5-bc88-6527e35fdb76)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/1.png)

После успешного создания и активации виртуального окружения, а также установки всех зависимостей Netbox, можно продолжить с настройкой и запуском Netbox.
Создадим БД и пользователя в ней.

[![image](https://github.com/user-attachments/assets/b545cae0-8361-465e-93e2-cf4f579dba9f)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/2.png)


[![image](https://github.com/user-attachments/assets/184cc4b9-6463-4ce3-a2bc-ba4f0dce20b9)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/3.png)

И завершим настройку запуском.

[![image](https://github.com/user-attachments/assets/16338a1d-3ab5-4da4-9622-3ccd68268712)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/4.png)

Теперь появилась возможность зайти в Netbox. Там добавляем наши устройства.

[![image](https://github.com/user-attachments/assets/d6888e03-19c1-43ac-b4cb-5281a8b9ebd6)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/5.png)

Затем с помощью скрипта перенаправляем сохранение логов и данных в файл.

```
ansible-inventory -v --list -y -i netbox_inventory.yml > nb_inventory.yml
```

Пишем файл inventory.yaml, содержащий информацию об устройствах для настройки ansible:

```
all:
  hosts:
    CHR1:
      ansible_host: 192.168.0.123
      ansible_user: admin
      ansible_password: 1111
    CHR2:
      ansible_host: 192.168.0.129
      ansible_user: admin
      ansible_password: 222
```

В конце настраиваем плейбук для автоматической настройки параметров, таких как NTP, OSPF, а также для сбора серийных номеров устройств.

```
- name: Configure CHR
  hosts: all
  tasks:
    - name: Collect serial number
      ansible.builtin.shell: "/system/routerboard/print"
      register: serial_output

    - name: Print serial
      ansible.builtin.debug:
        var: serial_output.stdout
```

Запускаем плейбук и тестируем связность устройств:

[![image](https://github.com/user-attachments/assets/803015ff-333b-437f-a320-c7c084e6dfdf)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/6.png)

[![image](https://github.com/user-attachments/assets/e55b5716-9428-4024-ab18-0b15ef044904)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab3/screenshots/7.png)

## Вывод

В ходе выполнения лабораторной работы была изучена работа с Ansible и Netbox, были собраны данные, конфигурации сетевых устройств.

