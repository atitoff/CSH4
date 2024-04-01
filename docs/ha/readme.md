# Home Assistant

* [установка](install.md)
* [MQTT триггер](mqtt_trigger.md)


```
apt-get remove -y --purge x11-common
apt-get autoremove -y --purge
apt-get install -y deborphan
deborphan | xargs dpkg -P # do this a bunch of times
```

### Установка Let's Encrypt и Duck DNS в Docker

<details><summary>Подробнее</summary>

docker-compose.yml
```yaml
version: '3.3'

services:
  duckdns:
    image: ghcr.io/linuxserver/duckdns
    container_name: duckdns
    environment:
      - PUID=1000 #optional
      - PGID=1000 #optional
      - TZ=Europe/Moscow
      - SUBDOMAINS=asasl.duckdns.org
      - TOKEN=407231f3-959e-4793-9d70-515cf9bd844c
      - LOG_FILE=false #optional
    volumes:
      - ./config:/config #optional
    restart: unless-stopped

  letsencrypt:
    image: linuxserver/swag
    container_name: letsencrypt
    cap_add:
      - NET_ADMIN
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Europe/Moscow
      - URL=asasl.duckdns.org
      - VALIDATION=http
      - EMAIL=mail@mail.ru #optional
      - EXTRA_DOMAINS=asasl.duckdns.org
    volumes:
      - ./config:/config
    ports:
      - 443:443
      - 80:80 #optional
    restart: unless-stopped
```

</details>