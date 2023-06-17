# Home Assistant

## Виртуальная машина KVM

На базе Debian 11

```
sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils libguestfs-tools genisoimage virtinst libosinfo-bin virt-manager
```

Добавляем пользователя в группы
```
sudo adduser alex libvirt
sudo adduser alex libvirt-qemu
```

Перегружаем и проверяем наличие пользователя в группах
```
newgrp libvirt
newgrp libvirt-qemu
id
```

Проверяем коннект к KVM серверу
```
virsh --connect qemu:///system
virsh --connect qemu:///system list --all
```

X11 серверная часть
```
sudo apt-get install xorg openbox
```

Устанавливаем на windows Xming server, запускаем

Далее в PuTTY

![image](https://user-images.githubusercontent.com/13304485/176812289-9811ce94-f167-4565-94e0-64438bd94efd.png)

Коннектимся из PuTTY и запускаем:
```
virt-manager
```

Появляется GUI

![image](https://user-images.githubusercontent.com/13304485/176993391-0b46efa3-5be6-4ada-bce8-3ef5a3a53f81.png)

### Make Network active and auto-restart

```
sudo virsh net-list --all
 Имя       Состояние    Автозапуск   Постоянный
-------------------------------------------------
 default   не активен   no           yes


sudo virsh net-start default
sudo virsh net-autostart default
```

### Настраиваем мост
``` sudo nano /etc/network/interfaces```

```bash

# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
#allow-hotplug ens32
#iface ens32 inet dhcp

auto br0
iface br0 inet dhcp
   bridge_ports ens32

```

#### Через nmcli

`sudo nmcli con show`
Then, add a new bridge called br0:
`sudo nmcli con add ifname br0 type bridge con-name br0`
Create a slave interface for br0 using eth0 NIC:
`sudo nmcli con add type bridge-slave ifname eth0 master br0`
Turn on br0 interface to get an IP via DHCP:
`sudo nmcli con up br0`
`sudo nmcli connection delete 'Wired connection 1'`
`sudo nmcli con show`
```
NAME                UUID                                  TYPE      DEVICE 
br0                 0877cdc2-4f10-4cdc-ac8d-fd4ed9d152e4  bridge    br0    
lo                  611f8710-7e23-4d23-a486-e4767d126b8d  loopback  lo     
bridge-slave-eth0   2202c9b7-0b24-4e7b-9e85-41e05eb2354a  ethernet  eth0  
```

### Создаем виртуалку

```
mkdir -vp ~/images/hassos-vm && cd ~/images/hassos-vm
wget https://github.com/home-assistant/operating-system/releases/download/8.2/haos_ova-8.2.qcow2.xz
virsh pool-create-as --name hassos --type dir --target ~/images/hassos-vm
xz -d -v haos_ova-8.2.qcow2.xz
```

```
sudo virt-install --import --name hassos \
--memory 2048 --vcpus 2 --cpu host \
--disk haos_ova-8.2.qcow2,format=qcow2,bus=virtio \
--network bridge=br0,model=virtio \
--graphics none \
--noautoconsole \
--boot uefi
```

## Cockpit
This installs  that can be accessed via hostIP:9090 and installs the virtual machine manager.
```
 sudo apt-get install cockpit
 sudo apt-get install cockpit-machines
 sudo apt-get install virt-viewer
```

### SSH
Пробрасываем временно снаружи 80 порт
Устанавливаем Let's Encrypt
Правим конфиг
```yaml
http:
  base_url: https://asasl.duckdns.org:8123
  ssl_certificate: /ssl/fullchain.pem
  ssl_key: /ssl/privkey.pem
```



![image](https://user-images.githubusercontent.com/13304485/177000877-e9fe1d8e-0dda-431d-9ab2-ed1e745d6af6.png)

![image](https://user-images.githubusercontent.com/13304485/177000951-747ee874-5a4e-418b-bd9e-30f4e7bce87b.png)

apk add qemu-guest-agent

sudo virsh edit hassos

Не забудьте добавить конфигурационный XML файл виртуальной машины следующий блок:

<channel type='unix'>

<target type='virtio' name='org.qemu.guest_agent.0'/>

</channel>
Добавляется он в секцию “Device”, после чего нужно сохранить конфигурацию и выполнить ребут машины.
