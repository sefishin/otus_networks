## Практическая работа №1. Router-on-a-Stick.

###  Задание:

  1. Построение сети и настройка основных параметров устройств;
  2. Создание VLAN и назначение портов;
  3. Настройка 802.1Q-транка между коммутаторами;
  4. Настройка сабинтерфейсов на маршрутизаторе.
  5. Проверка маршрутизации между VLAN.
  
### Решение:

 #### 1. Построить заданную топологию в Cisco Packet Tracer в соответствии с предоставленной схемой. Подключить нужные порты, произвести базовые настройки. 
  
  ![](https://github.com/sefishin/otus_networks/blob/master/labs/lab01/lab1.png)
  
 #### 2. Настройка VLAN и назначение портов на устройствах в соответствии с предоставленными таблицами.
  
  Addressing Table
  
  | Device | Interface |  IP Address  |  Subnet Mask  | Default Gateway |
  |:------:|:---------:|:------------:|:-------------:|:---------------:|
  | R1     | G0/0/1.3  | 192.168.3.1  | 255.255.255.0 | N/A             |
  |        | G0/0/1.4  | 192.168.4.1  | 255.255.255.0 | N/A             |
  |        | G0/0/1.8  | N/A          | N/A           | N/A             |
  | S1     | VLAN 3    | 192.168.3.11 | 255.255.255.0 | 192.168.3.1     |
  | S2     | VLAN 3    | 192.168.3.12 | 255.255.255.0 | 192.168.3.1     |
  | PC-A   | NIC       | 192.168.3.3  | 255.255.255.0 | 192.168.3.1     |
  | PC-B   | NIC       | 192.168.4.3  | 255.255.255.0 | 192.168.4.1     |

  VLAN Table
  
  | VLAN |    Name    |                      Interface Assigned                     |
  |:----:|:----------:|:-----------------------------------------------------------:|
  | 3    | Management | S1: VLAN 3 S2: VLAN 3 S1: F0/6                              |
  | 4    | Operations | S2: F0/18                                                   |
  | 7    | ParkingLot | S1: F0/2-4, F0/7-24, G0/1-2  S2: F0/2-17, F0/19-24, G0/1-2  |
  | 8    | Native     | N/A                                                         |  


 #### 3. Настройка 802.1Q-транка между коммутаторами. Для интерфейса f0/1 на обоих коммутаторах:
  
    interface FastEthernet0/1
    switchport trunk native vlan 8
    switchport trunk allowed vlan 3-4,8
    switchport mode trunk
 
 #### 4. Настройка сабинтерфейсов на маршрутизаторе:
 
    interface GigabitEthernet0/0/1.3
    description Default GW for VLAN 3
    encapsulation dot1Q 3
    ip address 192.168.3.1 255.255.255.0
  
    interface GigabitEthernet0/0/1.4
    description Default GW for VLAN 4
    encapsulation dot1Q 4
    ip address 192.168.4.1 255.255.255.0
  
    interface GigabitEthernet0/0/1.8
    description Default GW for VLAN 8
    encapsulation dot1Q 8 native
    no ip address
 
   Включение основного интерфейса:
 
    interface GigabitEthernet0/0/1
    no shutdown
 
  #### 5. Проверка маршрутизации между VLAN.
  
  ![](https://github.com/sefishin/otus_networks/blob/master/labs/lab01/ping.png)
 
 ###  Файлы конфигураций:
 -[R1_config](https://github.com/sefishin/otus_networks/blob/master/labs/lab01/R1_config)
 -[S1_config](https://github.com/sefishin/otus_networks/blob/master/labs/lab01/S1_config)
 -[S2_config](https://github.com/sefishin/otus_networks/blob/master/labs/lab01/S2_config)
 
  
  
