# Интерфейс DALI на базе ESP32ETH

[Сопряжение CLion c Arduino](../clion_arduino/readme.md)


### Принцип кодирования

Сначала преобразуем в манчестерский код, а потом сгенерируем последовательность для RMT.

The RMT is ESP32-specific and allows generation of accurate digital pulses with 12.5ns resolution.

Генерим последовательность как в примере с декодированием 10110


```python
import esp32
from machine import Pin

r = esp32.RMT(0, pin=Pin(18), clock_div=256)
# RMT(channel=0, pin=18, source_freq=80000000, clock_div=128)
r.write_pulses((269, 520, 520, 260, 260, 520, 260), start=1) 
# Send 1 for 416us, 0 for 832us, 1 for 832us, 0 for 416us, 1 for 416us, 0 for 832us, 1 for 416us
```

## Команды MQTT

Команда | MQTT | to ESP32 | from<br>ESP32 |
|----|----|----|----|
**Установить яркость светильника** 32 в 133     | dali/ha/set_level/32/130      | {01, 32, 133}
**Установить яркость группы** 12 в 254          | dali/ha/set_level_grp/12/254  | {02, 12, 254}
**Поиск существующих модулей**                  | dali/ha/find/12/254           | {02, 12, 254}     | {00 or 01}
**RAW** команды |
**Команда с приемом**                           | dali/ha/raw_r/addr/val        | {254, addr, val}  | {00 or 01}
**Команда без приема**                          | dali/ha/raw/addr/val          | {255, addr, val}
**Ответ**                                       | dali/ha/raw_ret/val           |                   | {00 or 01}




## Принципиальная схема

Так как модуль уже развязан от сети, то оптронов не нужно  
В качестве полевика подойдет SI2304DDS-T1-GE3  
В источнике питания BD139-16, BCP56-16T1G



![](esp_interface.svg)

