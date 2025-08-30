# Установка Pimox на Rock Pi 4a

Включаем обновления

```
sudo apt-get install -y wget
source /etc/os-release
export DISTRO="${VERSION_CODENAME}-stable"
wget -O - apt.radxa.com/$DISTRO/public.key | sudo apt-key add -
sudo apt-get update
```

```
sudo systemctl stop NetworkManager
nmcli dev status
Error: NetworkManager is not running.
sudo systemctl disable NetworkManager
```

```
auto lo
iface lo inet loopback

auto eth0
iface eth0 inet static
  address 192.168.1.80
  netmask 255.255.255.0
  network 192.168.1.0
  broadcast 192.168.1.255
  gateway 192.168.1.1
  dns-nameservers 192.168.1.1
```

`sudo ifup eth0`

reboot

echo "deb https://raw.githubusercontent.com/pimox/pimox7/master/ dev/" > /etc/apt/sources.list.d/pimox.list
curl https://raw.githubusercontent.com/pimox/pimox7/master/KEY.gpg | apt-key add -
apt update
apt install proxmox-ve (use a local attatched console! Network connections will be lost/reset during installation progress)