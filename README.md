# my-demo-rg2026
Настройка dhcp 
```
ip pool test 1
range 192.168.200.2-192.168.200.254
```
* Для настройки DHCP-сервера необходимо в режиме конфигурации ввести команду dhcp-server <NUMBER>
  * где NUMBER – номер сервера в системе маршрутизатора:
```
hq-rtr(config)#dhcp-server 1
hq-rtr(config-dhcp-server)#
```
* Привязываем ранее созданный POOL раздаваемых адресов с именем VLAN200 с номером DHCP-сервера в системе маршрутизатора 1:
```
hq-rtr(config-dhcp-server)#pool VLAN200 1
hq-rtr(config-dhcp-server-pool)
```
* Задаём основные параметры для раздачи DHCP сервером:
```
hq-rtr(config-dhcp-server-pool)#mask 24
hq-rtr(config-dhcp-server-pool)#gateway 192.168.200.1
hq-rtr(config-dhcp-server-pool)#dns 192.168.100.2
hq-rtr(config-dhcp-server-pool)#domain-name au-team.irpo
hq-rtr(config-dhcp-server-pool)#exit
hq-rtr(config-dhcp-server)#exit
```
* После настройки сервера необходимо указать, на каком интерфейсе маршрутизатор будет принимать пакеты DHCP Discover и отвечать на них предложением с IP-настройками:
  * в данном случае подинтерфейс с именем vl200 смотрит в сторону клиентской подсети (vlan200)
```
hq-rtr(config)#interface vl200 
hq-rtr(config-if)#dhcp-server 1
hq-rtr(config-if)#exit
hq-rtr(config)#write memory
Building configuration...

hq-rtr(config)#
```
