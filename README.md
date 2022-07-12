# Архитектура сетей
## Описание домашнего задания
1. Скачать и развернуть Vagrant-стенд
(https://github.com/erlong15/otus-linux/tree/network)
2. Построить следующую сетевую архитектуру:

Сеть office1
- 192.168.2.0/26 - dev
- 192.168.2.64/26 - test servers
- 192.168.2.128/26 - managers
- 192.168.2.192/26 - office hardware

Сеть office2
- 192.168.1.0/25 - dev
- 192.168.1.128/26 - test servers
- 192.168.1.192/26 - office hardware

Сеть central
- 192.168.0.0/28 - directors
- 192.168.0.32/28 - office hardware
- 192.168.0.64/26 - wif

Сеть InetRouter
- 192.168.255.0/30 - inet central


## Задание состоит из 2-х частей: теоретической и практической.

В теоретической части требуется:
- Найти свободные подсети
- Посчитать количество узлов в каждой подсети, включая
свободные
- Указать Broadcast-адрес для каждой подсети
- Проверить, нет ли ошибок при разбиении

В практической части требуется:
- Соединить офисы в сеть согласно логической схеме и настроить
роутинг
- Интернет-трафик со всех серверов должен ходить через inetRouter
- Все сервера должны видеть друг друга (должен проходить ping)
- У всех новых серверов отключить дефолт на NAT (eth0), который
vagrant поднимает для связи
- Добавить дополнительные сетевые интерфейсы, если потребуется
Рекомендуется использовать Vagrant + Ansible для настройки
данной схемы.

## Подготовка
Проверка версий среды:
```
root@yarkozloff:/otus/netlab# hostnamectl | grep "Operating System"
  Operating System: Ubuntu 20.04.3 LTS
root@yarkozloff:/otus/netlab# vboxmanage --version
6.1.26_Ubuntur145957
root@yarkozloff:/otus/netlab# vagrant --version
Vagrant 2.2.19
```
## Теоретическая часть
Из имеющихся данных рассчитываем все сети:
(IP калькулятор - https://ip-calculator.ru/)
+ Подсчитаем свободные сети:
![image](https://user-images.githubusercontent.com/69105791/178373670-2dd199a3-b7f0-4f6b-b577-548ae6320a4f.png)

## Практическая часть
Построим полную схему сети:
![image](https://user-images.githubusercontent.com/69105791/178373790-eac98209-b5e0-413f-ae9a-ee01c17d2aff.png)

Подготовим список серверов:
![image](https://user-images.githubusercontent.com/69105791/178376945-d7f9f46d-cb67-47ee-a6d5-94b3fd3b252f.png)


