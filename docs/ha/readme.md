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


### Mosquitto

```shell
sudo apt-get install mosquitto
mosquitto_passwd -b passwordfile mqtt
```

MqttBox - клиент для тестов
