# Home Assistant

## Установка

### Python

```shell
sudo apt-get update
sudo apt-get upgrade -y
sudo apt-get install -y libffi-dev libssl-dev libjpeg-dev zlib1g-dev autoconf build-essential libopenjp2-7 libtiff5 libsqlite3-dev
```

```shell
wget https://www.python.org/ftp/python/3.8.8/Python-3.8.8.tar.xz
tar -xf Python-3.8.8.tar.xz
cd Python-3.8.8
./configure --enable-optimizations --enable-loadable-sqlite-extensions
make -j 2
sudo make altinstall
```

### Homeassistant

```shell
sudo mkdir /srv/homeassistant
sudo chown homeassistant:homeassistant /srv/homeassistant
cd /srv/homeassistant
python3.8 -m venv .
source bin/activate

python3.8 -m pip install wheel
pip3.8 install homeassistant

hass
```

Создадим директорию для конфигов:  
`mkdir /srv/homeassistant/config`


`sudo nano /etc/systemd/system/hass.service`
```
[Unit]
Description=Home Assistant
After=network.target
[Service]
Type=simple
User=homeassistant
ExecStart=/srv/homeassistant/bin/hass -c /srv/homeassistant/config --log-file /srv/homeassistant/hass.log
[Install]
WantedBy=multi-user.target
```

```shell
sudo systemctl start hass
sudo systemctl status hass
```

```shell
● hass.service - Home Assistant
   Loaded: loaded (/etc/systemd/system/hass.service; disabled; vendor preset: enabled)
   Active: active (running) since Wed 2021-03-24 11:47:11 MSK; 1min 4s ago
 Main PID: 20434 (hass)
    Tasks: 11 (limit: 2330)
   Memory: 87.5M
   CGroup: /system.slice/hass.service
           └─20434 /srv/homeassistant/bin/python3.8 /srv/homeassistant/bin/hass -c /srv/homeassistant/config --log-file /srv/homeassistant

мар 24 11:47:11 ha systemd[1]: Started Home Assistant.
```

```shell
sudo systemctl enable hass
```

http://ha:8123

Скачать [Linux Debian 10 c Python 3.8.8](https://drive.google.com/file/d/1YNbDl3StzkifWjlsBz_FTdgOKYZsLp15/view?usp=sharing) (600M) для VMware  
login: homeassistant
password: bh0020

### Install Home Assistant Container



проверим название и версию Ubuntu

```shell
lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 20.04.2 LTS
Release:        20.04
Codename:       focal
```

Установим Docker

```shell
sudo apt update
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=armhf] https://download.docker.com/linux/ubuntu eoan stable"
sudo apt update
sudo apt install docker-ce docker-ce-cli docker-compose

# создадим директорию для конфигов
mkdir /home/alex/ha_config

sudo docker run --init -d \
  --name homeassistant \
  --restart=unless-stopped \
  -v /etc/localtime:/etc/localtime:ro \
  -v /home/alex/ha_config:/config \
  --network=host \
  homeassistant/home-assistant:stable
```


### Mosquitto

```shell
sudo apt install mosquitto mosquitto-clients
sudo mosquitto_passwd -c /etc/mosquitto/passwd alex
sudo nano /etc/mosquitto/conf.d/default.conf
```

```
allow_anonymous false
password_file /etc/mosquitto/passwd

# Plain MQTT protocol
listener 1883


listener 8083
protocol websockets
```

`sudo systemctl restart mosquitto`

MqttBox - клиент для тестов

## Виртуальная машина KVM

На базе Debian 11

```
sudo apt install qemu-kvm libvirt-clients libvirt-daemon-system bridge-utils libguestfs-tools genisoimage virtinst libosinfo-bin
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
Please note that you need to use the following command to connect to KVM server:
virsh --connect qemu:///system
virsh --connect qemu:///system list --all
```
