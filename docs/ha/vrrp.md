# Отказоустойчивый кластер на Linux с помощью VRRP
VRRP - протокол резервирования виртуальных маршрутизаторов, предназначен для повышения отказоустойчивости сервисов по сети или организации балансировки нагрузки между узлами. Отказоустойчивость достигается объединением нескольких узлов один виртуальным адресом, который переназначется следующему узлу, при отказе основного узла. В среде Linux для реализации VRRP используется демон Keepalived.

В данной статье будет рассмотрена только организация отказоустайчивости, без балансировки. Настройка будет производиться на серверах Debian 9 с адресами 192.168.120.1 - FreePBX1, 192.168.120.2 - FreePBX2, в качестве виртуального ip-адреса возьмем - 192.168.120.3

## Настройка FreePBX1

Установим keepalived

`sudo apt-get install keepalived`

<details><summary>Конфигурационный файл keepalived</summary>

`sudo nano /etc/keepalived/keepalived.conf`

```shell
########################
## VRRP configuration ##
########################

# Указываем VRRP istance (экземпляр). Например даем ему имя failover_test
vrrp_instance failover_test {

#Статус сервера в VRRP instance. Может быть MASTER или BACKUP

state MASTER

# Указываем интерфейс к которому будет привязан VRRP instance

interface eno1

# Указываем произвольно значение в интервале от 1 до 255,
# для того чтобы однозначно определить instance среди других,
# которые могут быть запущены на хосте. 
# Должен быть одинаков на всех хостах в instance.

virtual_router_id 10

# Приоритет хоста. Тот хост, который имеет больший приоритет,
# будет являться MASTER. По-умолчанию значение равно 100.

priority 110

# Указываем время в секундах между VRRP запросами между хостами в instance.
# По-умолчанию 1 секунда.

advert_int 4

# Authentication method: AH indicates ipsec Authentication Header.
# It offers more security than PASS, which transmits the
# authentication password in plaintext. Some implementations
# have complained of problems with AH, so it may be necessary
# to use PASS to get keepalived"s VRRP working.
#
# The auth_pass will only use the first 8 characters entered.

#Метод аутентификации. AH - ipsec Authentication Header
#                       PASS - пароль в открытом виде.
# AH более безопасен и рекомендуется использовать его,
#но в некоторых реализациях keepalived AH метод может не работать,
#тогда необходимо использовать PASS.

authentication {
auth_type AH
auth_pass 1111
}

# VRRP запросы обычно являются мультикастовыми. Если вы хотите ограничить
# устройства, которые будут видеть эти запросы, можно использовать директиву
# unicast_peer, где указываются IPv4 или IPv6 адреса хостов в instance.

unicast_peer {
192.168.120.2
}

# Указываем общий виртуальный ip-адрес для членов VRRP instance.
# Можем указать какому интерфейсу он будет назначен, а так же с
# помощью директивы "label" указать для него описание.

    virtual_ipaddress {
    192.168.120.3/21 brd 192.168.127.255 dev eno1 label eno1:vip 
}

}
```

</details>

Запустим демон keepalived

```
sudo systemctl start keepalived
sudo systemctl enable keepalived
```

Переходим к настройке второго хоста.

##Настройка FreePBX2

Установим keepalived

root@FreePBX2:~# apt-get install keepalived



<details><summary>Конфигурационный файл keepalived</summary>

root@FreePBX2:~# cat /etc/keepalived/keepalived.conf

```shell
########################
## VRRP configuration ##
########################

# Указываем VRRP istance (экземпляр). Например даем ему имя failover_test
vrrp_instance failover_test {

# Статус сервера в VRRP instance. Может быть MASTER или BACKUP
# Устанавливаем статус BACKUP

state BACKUP

# Указываем интерфейс к которому будет привязан VRRP instance

interface eno1

# Указываем произвольно значение в интервале от 1 до 255,
# для того чтобы одназначно определить instance среди других,
# которые могут быть запущены на хосте. 
# Должен быть одинаков на всех хостах в instance.

virtual_router_id 10

# Приоритет хоста. Тот хост, который имеет больший приоритет,
# будет являться MASTER. По-умолчанию значение равно 100.
# Устанавливаем приоритет меньше, чем на хосте MASTER

priority 100

# Указываем время в секундах между VRRP запросами между хостами в instance.
# По-умолчанию 1 секунда.

advert_int 4

# Authentication method: AH indicates ipsec Authentication Header.
# It offers more security than PASS, which transmits the
# authentication password in plaintext. Some implementations
# have complained of problems with AH, so it may be necessary
# to use PASS to get keepalived"s VRRP working.
#
# The auth_pass will only use the first 8 characters entered.

# Метод аутентификации. AH - ipsec Authentication Header
#                       PASS - пароль в открытом виде.
# AH более безопасен и рекомендуется использовать его,
# но в некоторых реализациях keepalived AH метод может не работать,
# тогда необходимо использовать PASS.

authentication {
auth_type AH
auth_pass 1111
}

# VRRP запросы обычно являются мультикастовыми. Если вы хотите ограничить
# устройства, которые будут видеть эти запросы, можно использовать директиву
# unicast_peer, где указываются IPv4 или IPv6 адреса хостов в instance.

unicast_peer {
192.168.120.1
}

# Указываем общий виртуальный ip-адрес для членов VRRP instance.
# Можем указать какому интерфейсу он будет назначен, а так же с
# помощью директивы "label" указать для него описание.

virtual_ipaddress {
    192.168.120.3/21 brd 192.168.127.255 dev eno1 label eno1:vip 
}

}
```

</details>

Запустим демон keepalived

```
sudo systemctl start keepalived
sudo systemctl enable keepalived
```

Проверяем работу VRRP instance
доставим

sudo yum install net-tools

На FreePBX1 проверим наличие общего виртуального ip-адреса

```
ip a
eno1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.120.1  netmask 255.255.248.0  broadcast 192.168.127.255
        inet6 fe80::a6bf:1ff:fe46:648f  prefixlen 64  scopeid 0x20<link>
        ether a4:bf:01:46:64:8f  txqueuelen 1000  (Ethernet)
        RX packets 6009365  bytes 626018596 (597.0 MiB)
        RX errors 0  dropped 310282  overruns 0  frame 0
        TX packets 18915  bytes 5546729 (5.2 MiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device memory 0x9cb00000-9cbfffff

eno1:vip: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.120.3  netmask 255.255.248.0  broadcast 192.168.127.255
        ether a4:bf:01:46:64:8f  txqueuelen 1000  (Ethernet)
        device memory 0x9cb00000-9cbfffff
```

Теперь отключим интерфейс eth0 и посмотрим получит ли FreePBX2 виртуальный ip-адрес

`sudo ip link set dev eth0 down`

Подождем пока VRRP запросы пройдут

```
sudo ip a
eth0: flags=4163  mtu 1500
        inet 192.168.120.2  netmask 255.255.255.0  broadcast 10.25.128.255
        inet6 fe80::216:3eff:fecb:ec1b  prefixlen 64  scopeid 0x20
        ether 00:16:3e:cb:ec:1b  txqueuelen 1000  (Ethernet)
        RX packets 13380  bytes 20350376 (19.4 MiB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 7617  bytes 522763 (510.5 KiB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0:vip: flags=4163  mtu 1500
        inet 192.168.120.3  netmask 255.255.255.255  broadcast 0.0.0.0
        ether 00:16:3e:cb:ec:1b  txqueuelen 1000  (Ethernet)
```

FreePBX2 получил виртуальный ip-адрес
Как только FreePBX1 станет вновь доступной, то виртуальный ip-адрес перейдет снова на нее так как она указана с более высоким приоритетом.