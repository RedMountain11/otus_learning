# Лабораторная работа. Базовая настройка коммутатора
## 1. Топология
![](https://github.com/RedMountain11/otus_learning/blob/main/homeworks/JPG/Лабораторная%201%20-%20топология.png)

|Устройство|Интерфейс|IP-адрес \ префикс|
|----------|--------|--------|
|s1|VLAN1|192.168.1.2/24|
|PC-A|NIC|192.168.1.10/24|

## 2. Задачи
1. Проверка конфигурации коммутатора по умолчани
2. Создание сети и настройка основных параметров устройства
+ Настроить базовые параметры коммутатора.
+ Настроить IP-адрес для ПК.
3. Проверка сетевых подключений
+ Отобразить конфигурацию устройства.
+ Протестировать сквозное соединение, отправив эхо-запрос.
+ Протестировать возможности удаленного управления с помощью Telnet.

## 3. Решение
I. Создание сети и проверка настроек коммутатора по умолчанию
1. Создан коммуатор, PC. К коммутатору подключен консольный кабель.
2. Осуществлено подключение по консольному порту, переход из пользовательского режима в EXEC enable.
3. Вбита команда show running-config:
   + Сколько интерфейсов FastEthernet имеется на коммутаторе 2960? Ответ: 24
   + Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960? Ответ: 2
   + Каков диапазон значений, отображаемых в vty-линиях? Ответ: 0-4, 5-15
4. Изучите файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM).
   + Вопрос: почему появляется это сообщение? Ответ: вопрос не понятен. Какое сообщение?
5. Изучите характеристики SVI для VLAN 1:
   + Назначен ли IP-адрес сети VLAN 1? Ответ: да
   + Какой MAC-адрес имеет SVI? Возможны различные варианты ответов. Ответ: 0001.c700.4c0b.
   + Данный интерфейс включен? Ответ: да.
6. Изучите IP-свойства интерфейса SVI сети VLAN 1:
   + Какие выходные данные вы видите? Ответ:
       - Ответ:
```Vlan1 is up, line protocol is up
Hardware is CPU Interface, address is 0001.c700.4c0b (bia 0001.c700.4c0b)
Internet address is 192.168.1.2/24
MTU 1500 bytes, BW 100000 Kbit, DLY 1000000 usec,
reliability 255/255, txload 1/255, rxload 1/255
Encapsulation ARPA, loopback not set
ARP type: ARPA, ARP Timeout 04:00:00
Last input 21:40:21, output never, output hang never
Last clearing of "show interface" counters never
Input queue: 0/75/0/0 (size/max/drops/flushes); Total output drops: 0
Queueing strategy: fifo
Output queue: 0/40 (size/max)
5 minute input rate 0 bits/sec, 0 packets/sec
5 minute output rate 0 bits/sec, 0 packets/sec
1682 packets input, 530955 bytes, 0 no buffer
Received 0 broadcasts (0 IP multicast)
0 runts, 0 giants, 0 throttles
0 input errors, 0 CRC, 0 frame, 0 overrun, 0 ignored
563859 packets output, 0 bytes, 0 underruns
0 output errors, 23 interface resets
0 output buffer failures, 0 output buffers swapped out
```
   + Под управлением какой версии ОС Cisco IOS работает коммутатор? Ответ: Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
   + Как называется файл образа системы? Ответ:  C2960-LANBASEK9-M
7. Изучите свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A.
  + Интерфейс включен или выключен? Ответ: интерфейс включён (включил ранее)
  + Что нужно сделать, чтобы включить интерфейс? Ответ: в режиме конфигурации интерфейса набрать "no shutdown"
  + Какой MAC-адрес у интерфейса? Ответ: 00e0.a346.e906
  + Какие настройки скорости и дуплекса заданы в интерфейсе? Ответ: Дуплекс, 100 МБ\с
8. Какое имя присвоено образу Cisco IOS? Ответ: 2960-lanbasek9-mz

II. Настройка базовых параметров сетевых устройств
1. Настройте базовые параметры коммутатора. Выполнение: выполнено
2. Назначьте IP-адрес интерфейсу SVI на коммутаторе. Благодаря этому вы получите возможность удаленного управления коммутатором. Выполнение: выполнено
3. Для чего нужна команда login? Ответ:  чтобы активировать (применить настройки) способа входа.
4. Настройте IP-адрес на компьютере PC-A. Выполнение: выполнено
5. Отобразите конфигурацию коммутатора. Выполнение:

```
Unauthorized access is strictly prohibited.

User Access Verification

Password: 
Password: 

S1>en
Password: 
S1#show run
Building configuration...

Current configuration : 1378 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname S1
!
enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
enable password 7 0832494B3609040401
!
!
!
no ip domain-lookup
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 ip address 192.168.1.2 255.255.255.0
!
banner motd ^C
Unauthorized access is strictly prohibited.^C
!
!
!
line con 0
 password 7 0822455D0A16
 logging synchronous
 login
!
line vty 0 4
 password 7 0822455D0A16
 login
 transport input telnet
line vty 5 15
 password 7 0822455D0A16
 login
!
!
!
!
end
```

6. Протестируйте сквозное соединение, отправив эхо-запрос. Выполнение: выполнено, работает.
7. Проверьте удаленное управление коммутатором S1. Выполнение: выполнено, работает.
   
[Ссылка на лабораторную](./config'n'lab/)
