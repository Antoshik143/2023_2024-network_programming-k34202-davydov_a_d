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
Создали новую виртуальную машину с данными параметрами:

![Настройка 1](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/5.png)
![Настройка 2](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/6.png)

Добавили свой публичный ключ на созданную в облаке машину.

![Ключи](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/7.png)

### 3. Настройка VPN сервера на машине в Yandex Cloud.
Подключение к удаленной машине.
![Подключение](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/8.png)

На удаленной машине установили Ansible и пакет pip.

![Пакеты](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/9.png)

Для создания VPN сервера был выбран OpenVPN Access Server. Его приемуществом является возможноть работы через удобный графический интерфейс.

Для его установки воспользуемсая оригинальной инструкцией с сайта openvpn.com для Ubuntu 22. Последовательно выполним следующие команды:

```apt update && apt -y install ca-certificates wget net-tools gnupg
wget https://as-repository.openvpn.net/as-repo-public.asc -qO /etc/apt/trusted.gpg.d/as-repository.asc
echo "deb [arch=amd64 signed-by=/etc/apt/trusted.gpg.d/as-repository.asc] http://as-repository.openvpn.net/as/debian jammy main">/etc/apt/sources.list.d/openvpn-as-repo.list
apt update && apt -y install openvpn-as
```
После выполнения этих команд получаем сообщение:

![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/10.png)


Переходим по ссылке https://*публичный_ip_сервера*:943/admin. И попадаем в меню авторизации, вводим выданный логин и пароль.
В настройках сети выбираем TCP и указываем 443 порт.
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/11.png)

В настройках VPN отключаем TLS.
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/12.png)

В User Permitions создаем нового пользователя и разрешаем автоматический вход.
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/13.png)

Во вкладке User Profiles надимаем New Profile и начинается загрузка .ovpn файла.
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/14.png)

Подробный статус о настроенном сервере
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/15.png)

### 4. Подключение CHR.

В WinBox перещди в Files и закинули скаченный файл конфигурации.
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/16.png)

Через терминал импортируем сертификаты из файла, используя команду <code>certificate import file-name=*название_файла*</code>.

Создали новый интерфейс:     

* Connect To - публичный ip сервера
* Port - 443
* Mode - ip
* Protocol - tcp
* User - ros
* Password - отсутствует
* Certeficate - ранее импортированный сертификат, оканчивающийся на 1

И нажали Apply:

![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/17.png)

Генерируемый трафик

![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/18.png)

Соединение установлено. Проверили связанность, пропинговав сервер по внутреннему ip-адресу:
![image](https://github.com/Antoshik143/2023_2024-network_programming-k34202-davydov_a_d/blob/main/lab1/pictures/19.png)


## Вывод:
В результате выполнения работы было выполнено развертывание виртуальной машины на базе платформы Yandex.Cloud с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox.
