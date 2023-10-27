#### University: [ITMO University](https://itmo.ru/ru/)
##### Faculty: [FICT](https://fict.itmo.ru)
##### Course: [Network Programming](https://itmo-ict-faculty.github.io/network-programming/)

Group: K34202

Author: Davydov Anton Dmitrievich

Lab: Lab1

Date of create: 06.10

Date of finished: 27.10

## Отчёт по лабораторной работе №1 "Установка CHR и Ansible, настройка VPN"

**Цель работы:** развертывание виртуальной машины на базе платформы Yandex Cloud с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox.

**Ход работы:**

### 1. Создание вирутальной машины с RouterOS и подключение через WinBox.

С официального сайта [Mikrotik](https://mikrotik.com/download/archive) скачали образ диска .vdi. Создали виртуальную машину, используя Virtualbox и ранее скачанный образ, выбрали тип сети - Сетевой мост и Разрешить всё.

![Настройки сети](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/1.png)

Подключение к запущенной виртуальной машине по ssh под логином admin.

![Подключение к тачке](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/2.png)

Также для удобства мы подключились к машине через WinBox

![Подключение к тачке через WinBox](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/3.png)

Результат подключения
![Подключение WinBox](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/4.png)

### 2. Создание вирутальной машины Ubuntu в Yandex Cloud.