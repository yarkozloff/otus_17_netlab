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
- 192.168.0.64/26 - wifi

Сеть InetRouter
- 192.168.255.0/30 - inet central


### Задание состоит из 2-х частей: теоретической и практической.

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

Рекомендуется использовать Vagrant + Ansible для настройки данной схемы.

## Подготовка
Проверка версий среды:
```
root@yarkozloff:/otus/netlab# hostnamectl | grep "Operating System"
  Operating System: Ubuntu 20.04.3 LTS
root@yarkozloff:/otus/netlab# vboxmanage --version
6.1.26_Ubuntur145957
root@yarkozloff:/otus/netlab# vagrant --version
Vagrant 2.3.0
```
## Теоретическая часть
Из имеющихся данных рассчитываем все сети:
(IP калькулятор - https://ip-calculator.ru/)
+ Построим таблицу топологии:
![image](https://user-images.githubusercontent.com/69105791/187277329-d86e2842-9fb8-42fe-895b-e68d985f63c9.png)

Свободные сети:
- 192.168.10.16/28
- 192.168.10.48/28
- 192.168.10.80/28
- 192.168.10.96/28
- 192.168.10.112/28
- 192.168.10.128/25
- 192.168.255.4/30
- 192.168.255.8/29
- 192.168.255.16/28
- 192.168.255.32/27
- 192.168.255.64/26
- 192.168.255.128/26
- 192.168.255.192/26

## Практическая часть
Добавляем в Vagrantfile дополнительные машины: Office1serv, Office1router, Office2router, Office2server. Убираем  NAT на всех узлах, кроме Inetrouter. Добавляем конфигурацию интерфейсов ВМ шлюзы. В параметрах ядра изменяем net.ipv4.conf.all.forwarding=1. Отключаем маршрут по умолчанию. echo "DEFROUTE=no" >> /etc/sysconfig/network-scripts/ifcfg-eth0. Добавляем дефолтный маршрут на другой порт. Настраиваем статические маршруты. 
### Тестирование
