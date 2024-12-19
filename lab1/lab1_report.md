University: [ITMO University](https://itmo.ru/ru/)

Faculty: [FICT](https://fict.itmo.ru)

Course: [Introduction in routing](https://github.com/itmo-ict-faculty/introduction-in-routing)

Year: 2024/2025

Group: K34212

Author: Shagvalieva Ekaterina Albertovna

Lab: Lab1

Date of create: 26.09.2024

Date of finished: 27.09.2024

# Лабораторная работ №1 "Установка CHR и Ansible, настройка VPN"

## Цель работы

Целью данной работы является развертывание виртуальной машины на базе платформы Microsoft Azure с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox.

## Ход работы

Для начала работы в Yandex.Cloud была создана виртуальная машина Ubuntu.

![https://github.com/user-attachments/assets/665643d7-de62-4a73-a92f-7fc8fff4bca0](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab1/screenshots/1.png)

К созданной виртуальной машине было выполнено подключение.

[![image](https://github.com/user-attachments/assets/9c5681ef-593f-437b-9a67-930d43c39361)](https://github.com/disnexide/2024_2025-network_programming-k34212-shagvalieva_e_a/blob/main/lab1/screenshots/2.png)

Были установлены python и ansible.

![image](https://github.com/user-attachments/assets/bb166d53-d049-4c6e-bee7-297c7f6ab0c6)

Затем с помощью VirtualBox была создана виртуальная машина RouterOS.

![image](https://github.com/user-attachments/assets/696f53ab-8a22-4172-94eb-7f66d9246d6e)

После настройки виртуального жесткого диска и нужных параметров соединения в настройках, виртуальная машина была запущена, на экран выведен выданный ей ip-адрес.

![image](https://github.com/user-attachments/assets/3fe93a86-fbcc-46c3-9b67-93c0bedd4652)

Через программу WinBox было выполнено подключение через выданный ранее ip-адрес.

![image](https://github.com/user-attachments/assets/ca0b326d-6054-4521-be31-9d1176e25e81)

С помощью интерфейса было настроено покдлючение wireguard - выбирано название и порт, ключи сгенерировалось автоматически.

![image](https://github.com/user-attachments/assets/dac8fbbe-cf79-4c33-9106-64b3700352fd)

Во вкладке "addresses" был добавлен адрес, который будет присвоен клиенту.

![image](https://github.com/user-attachments/assets/19947a0d-49c4-4e00-81a0-489f5aaa5769)

Также был настроен peer - в качестве ключа вставлен только что сгенерированный (при первоначальной настройке).

![image](https://github.com/user-attachments/assets/e21e31fa-9ba4-4401-9ebf-93ab40399119)

После этого на виртуальной машине Ubuntu были сгенерированы ключи.

![image](https://github.com/user-attachments/assets/f6ffea5c-d098-463a-9ed0-35e53601373e)

Затем приватный ключ интерфейса и публичный ключ пира были вставлены в конфигурационный файл wireguard.

![image](https://github.com/user-attachments/assets/09a8a8eb-c1a4-4bb3-ac24-371524087edd)

После этих шагов подключение должно заработать. Проверка:

1) Доступ ко внешней сети с ВМ Ubuntu
   
![image](https://github.com/user-attachments/assets/c835b360-c5a8-4137-b46c-7b30f3ce4d3d)

2) доступ ко внешней сети RouterOS
   
![image](https://github.com/user-attachments/assets/e0c901f4-0196-4b99-805a-b0bb6f4f7cba)

3) Настроенная в работе связь между сервером и клиентом
   
![image](https://github.com/user-attachments/assets/9e6b8760-9701-4032-9c18-ecc991a1c72f)


## Выводы
В ходе лабораторной работы были подняты две виртуальные машины на локальном компьютере и в облаке и настроено VPN соединение wireguard. Сложности в основном возникли в первой части работы - настройке вм на облаке, все остальное делалось с помощью понятных инструкций и документаций.




