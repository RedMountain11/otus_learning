## 1. Топология

![](https://github.com/RedMountain11/otus_learning/blob/8d6d57ebfb550e04f0884b2a4e989656d563ec43/homeworks/homework4/%D0%A2%D0%9E%D0%BF%D0%BE%D0%BB%D0%BE%D0%B3%D0%B8%D1%8F%20IPv6.jpg)
|Устройство|Интерфейс|IPv6-адрес|Link local | IPv6-адрес|Длина префикса|
|----------|--------|--------|----------|--------|--------|
|R1|G0/0/0|2001:db8:acad:a::1|fe80::1|64|-|
||G0/0/1|2001:db8:acad:1::1|fe80::1|64|-|
|S1|VLAN 1|2001:db8:acad:1::b|fe80::b|64|-|
|PC-A|NIC|2001:db8:acad:1::3|SLACC|64|fe80::1|
|PC-B|NIC|2001:db8:acad:a::3|SLACC|64|fe80::1|


## 2. Задачи
- Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
- Часть 2. Ручная настройка IPv6-адресов
- Часть 3. Проверка сквозного соединения
- 
- ## 3. Решение
1. Настроен R1: (выгрузка собрана после полного выполнения ДЗ - поэтому LLA уже имеет статический кастомный адрес)
```
R1#show ipv6 interface brief
FastEthernet0/0            [up/up]
    FE80::1
    2001:DB8:ACAD:A::1
FastEthernet0/1            [up/up]
    FE80::1
    2001:DB8:ACAD:1::1
Vlan1                      [administratively down/down]
    unassigned
R1#
```
2. Настроен IPv6-SVI на коммутаторе:
```
   Switch#show ipv6 interface brief
FastEthernet0/1            [down/down]
FastEthernet0/2            [down/down]
FastEthernet0/3            [down/down]
FastEthernet0/4            [down/down]
FastEthernet0/5            [up/up]
FastEthernet0/6            [up/up]
FastEthernet0/7            [down/down]
FastEthernet0/8            [down/down]
FastEthernet0/9            [down/down]
FastEthernet0/10           [down/down]
FastEthernet0/11           [down/down]
FastEthernet0/12           [down/down]
FastEthernet0/13           [down/down]
FastEthernet0/14           [down/down]
FastEthernet0/15           [down/down]
FastEthernet0/16           [down/down]
FastEthernet0/17           [down/down]
FastEthernet0/18           [down/down]
FastEthernet0/19           [down/down]
FastEthernet0/20           [down/down]
FastEthernet0/21           [down/down]
FastEthernet0/22           [down/down]
FastEthernet0/23           [down/down]
FastEthernet0/24           [down/down]
GigabitEthernet0/1         [down/down]
GigabitEthernet0/2         [down/down]
Vlan1                      [administratively down/down]
    FE80::B
    2001:DB8:ACAD:1::B
   ```
3. Проверена IP-конфигурация PC-B без автоконфигурирования по подписке на маршутизатор:
![](https://github.com/RedMountain11/otus_learning/blob/af3dd448a6cd78c5b413f09ba63e6a0f5e51f0a6/homeworks/homework4/pickchers/PC-B%20%D0%B0%D0%B4%D1%80%D0%B5%D1%81%20%D0%BD%D0%B5%20%D0%BD%D0%B0%D0%B7%D0%BD%D0%B0%D1%87%D0%B5%D0%BD.jpg)
4. Настроен IPv6 unicast-routing на маршрутизаторе, проверена конфигурация на PC-B:
![](https://github.com/RedMountain11/otus_learning/blob/af3dd448a6cd78c5b413f09ba63e6a0f5e51f0a6/homeworks/homework4/pickchers/PC-B%20%D0%B0%D0%B4%D1%80%D0%B5%D1%81%20%D0%BD%D0%B0%D0%B7%D0%BD%D0%B0%D1%87%D0%B5%D0%BD!.jpg)
5. Проверено сквозное соединение:
- PC-A -> LLA fa0/1 R1:
 ```
Cisco Packet Tracer PC Command Line 1.0
C:\>ping fe80::1

Pinging fe80::1 with 32 bytes of data:

Reply from FE80::1: bytes=32 time<1ms TTL=255
Reply from FE80::1: bytes=32 time<1ms TTL=255
Reply from FE80::1: bytes=32 time<1ms TTL=255
Reply from FE80::1: bytes=32 time<1ms TTL=255

Ping statistics for FE80::1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```
- PC-A -> интерфейс управления SVI S1:
```
C:\>ping 2001:db8:acad:1::b

Pinging 2001:db8:acad:1::b with 32 bytes of data:

Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255
Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255
Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255
Reply from 2001:DB8:ACAD:1::B: bytes=32 time<1ms TTL=255

Ping statistics for 2001:DB8:ACAD:1::B:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

```
- PC-A -> PC-B:
```
C:\>tracert FE80::2D0:97FF:FE9C:713

Tracing route to FE80::2D0:97FF:FE9C:713 over a maximum of 30 hops: 

  1   *         *         *         Request timed out.
  2   *         
Control-C
^C
C:\>
C:\>tracert 2001:DB8:ACAD:A::3

Tracing route to 2001:DB8:ACAD:A::3 over a maximum of 30 hops: 

  1   0 ms      0 ms      0 ms      2001:DB8:ACAD:1::1
  2   0 ms      0 ms      0 ms      2001:DB8:ACAD:A::3

Trace complete.
```
- PC-B -> PC-A
```
C:\>ping  2001:DB8:ACAD:1::3

Pinging 2001:DB8:ACAD:1::3 with 32 bytes of data:

Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127
Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127
Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127
Reply from 2001:DB8:ACAD:1::3: bytes=32 time<1ms TTL=127

Ping statistics for 2001:DB8:ACAD:1::3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

```
- PC-B -> на LLA fa0/0 R1:
```
  C:\>ping fe80:01
Ping request could not find host fe80:01. Please check the name and try again.
Reply from FE80::1: bytes=32 time<1ms TTL=255

Ping statistics for FE80::1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms

C:\>  
```
6. Вопросы для повторения
    1. Почему обоим интерфейсам Ethernet на R1 можно назначить один и тот же локальный адрес канала — FE80::1?
    2. Какой идентификатор подсети в индивидуальном IPv6-адресе 2001:db8:acad::aaaa:1234/64?
