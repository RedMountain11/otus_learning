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
3. Проверена IP-конфигурация PC-B без автоконфигурирования по полписке на маршутизатор:
4. 
