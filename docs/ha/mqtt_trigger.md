# MQTT триггер в автоматизациях Home Assistant
mqtt — это один из триггеров которые можно использовать в автоматизациях Home Assistant (список всех триггеров).

С помощью этого триггера можно запустить автоматизацию по событию в MQTT брокере.

Пример автоматизации
```yaml
automation:
  - trigger:
      platform: mqtt
      topic: sensor/temperature
    action:
      service: system_log.write
      data:
        message: mqtt event
```

Это автоматизация будет запускаться при любом обновлении топика `sensor/temperature`.
Если отправить в топик значение `22.7`, то в логе можно будет увидеть сообщение mqtt `event`.

![](mqtt_trigger1.png)

Если отправить еще одно сообщение 22.7 в этот топик, то в логе появится еще одна запись. Автоматизация запускатся при любом обновлении топика, даже если значение которое пришло в топик ровно такое же как приходило в прошлый раз.

## Поле `payload`
Можно сделать чтобы автоматизация запускалась только в случае если топик приходит какое-то определенное значение. Вот пример:

```yaml
automation:
  - trigger:
      platform: mqtt
      topic: sensor/switch
      payload: "on"
    action:
      service: system_log.write
      data:
        message: mqtt event
```
Эта автоматизация запустится не при любом изменении топика sensor/switch, а только если в этот топик придет строка on.
(При использовании строк on и off в yaml их нужно обязательно брать в кавычки)

## Поле `encoding`
Обычно поле encoding использовать не нужно. Если не указать поле encoding, это то же самое что явно сказать encoding: "utf-8". При работе со строками и цифрами это как раз то что нужно. Но в случае работы с бинарными данными (например, если значение топика — это изображение), нужно явно указать encoding: '':

```yaml
automation:
  - trigger:
      platform: mqtt
      topic: camera/image
      encoding: ''
    action:
      ...
```

## Переменная `trigger`
После того как mqtt триггер сработал в блоках condition и action становится доступна специальная переменная с именем trigger. Вот пример автоматизации которая записывает значение этой переменной в лог:

```yaml
automation:
  - trigger:
      platform: mqtt
      topic: sensor/temperature
    action:
      service: system_log.write
      data:
        message: "{{ trigger }}"
```
Если отправить в топик sensor/temperature значение 22.7, то в логе будет видно что содержится в переменной trigger:

![](mqtt_trigger2.png)

```python
{
    'platform': 'mqtt',
    'topic': 'sensor/temperature',
    'payload': '22.7',
    'qos': 0,
    'description': 'mqtt topic sensor/temperature',
    'payload_json': 22.7
}
```
В том случае если значение топика — это json, то в поле payload_json будет находится разобранный json.

## Примеры автоматизаций
### Включение и выключение switch на основании данных из топика
Вот автоматизация, которая включает вентилятор если в топик devices/fan прилетает значение 1 и выключает вентилятор если в топик приходит значение 0:
```yaml
automation:
  - trigger:
      platform: mqtt
      topic: devices/fan
    action:
      - choose:
          - conditions:
              - condition: template
                value_template: '{{ trigger.payload == "1" }}'
            sequence:
              - service: switch.turn_on
                entity_id: switch.fan
          - conditions:
              - condition: template
                value_template: '{{ trigger.payload == "0" }}'
            sequence:
              - service: switch.turn_off
                entity_id: switch.fan
```

### Автоматизация света в туалете с помощью датчика движения
Это пример как можно сделать авто включение-выключение света в туалете с помощью датчика движения (можно использовать разные датчики движения, например "Aqara human body movement and illuminance sensor").

В первую очередь это пример работы MQTT триггера, есть разные способы как делать автоматизацию света, тут показыается пример использования сырых событий от датчика который подключен к Home Assistant через zigbee2mqtt.

```yaml
timer:
  toilet:

automation:
  - alias: Turn on light in the toilet by aqara sensor motion
    trigger:
      platform: mqtt
      topic: zigbee2mqtt/0x00158d0004518e15
    condition:
      condition: template
      value_template: "{{ trigger.payload_json.occupancy }}"
    action:
      - service: light.turn_on
        data:
          entity_id: light.0xccccccfffe00418e
          brightness: "{% if is_state('binary_sensor.night', 'on') %}1{% else %}255{% endif %}"
      - service: timer.cancel
        data:
          entity_id: timer.toilet
      - service: timer.start
        data:
          entity_id: timer.toilet
          duration: "0:05:00"

  - alias: Turn off light in the toilet by timer
    trigger:
      - platform: event
        event_type: timer.finished
        event_data:
          entity_id: timer.toilet
    action:
      - service: light.turn_off
        data:
          entity_id: light.0xccccccfffe00418e
          transition: 5
```