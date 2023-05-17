# MQTT-GPIO

<img align="left"  src="nt_pad.png">


https://www.cdebyte.com/products/NT1-B

![](gpio1.svg)

## Первоначальная настройка модуля NT1-B

<details><summary>Настройка модуля</summary>

Первоначально модуль сидит на статическом адресе 192.168.3.3
настраиваем сеть компа и заходим

![](nt1b_mqtt_settings.png)

Настоятельно рекомендую настроить именно автоматическое получение адреса по DHCP.

Устанавливаем там где 0, нужный нам порядковый номер модуля и нажимаем submit,
пароль для сохранения 123456 после чего перезагружаем по питанию.

В сети его потом можно будет найти по доменному имени MAC адресу:
![](mac-domain.png)

</details>

## Прямые команды

Передаются в строковом виде ASCII

![direct_command.svg](direct_command.svg)


## Хранение информации о портах и их последующая компиляция

[Прошивка программы](write_fw/readme.md)

<details><summary>Подробнее</summary>

```yaml
0: [ "button", "output", "led_button_led", "gpio_exti15" ]                         # PB15
1: [ "button", "output", "led_button", "gpio_exti14" ]                             # PB14
2: [ "button", "output", "led_button_led", "gpio_exti12" ]                         # PB12
3: [ "button", "output", "led_button", "gpio_exti10" ]                             # PB10
4: [ "button", "output", "led_button_led", "tim3_ch4", "gpio_exti1" ]              # PB1
5: [ "button", "output", "led_button", "tim3_ch3", "gpio_exti0" ]                  # PB0
6: [ "button", "output", "led_button_led", "gpio_exti13" ]                         # PB13
7: [ "button", "output", "led_button", "gpio_exti11" ]                             # PB11
8: [ "button", "output", "led_button_led", "gpio_exti2" ]                          # PB2
9: [ "button", "output", "led_button" , "tim3_ch2", "gpio_exti7" ]                 # PA7
10: [ "button", "output", "led_button_led", "tim3_ch1", "gpio_exti6" ]             # PA6
11: [ "button", "output", "led_button", "gpio_exti8" ]                             # PB8
12: [ "button", "output", "led_button_led", "gpio_exti7" ]                         # PB7
13: [ "button", "output", "led_button", "gpio_exti4" ]                             # PB4
14: [ "button", "output", "led_button_led", "gpio_exti5" ]                         # PA5
15: [ "button", "output", "led_button", "gpio_exti9" ]                             # PB9
16: [ "button", "output", "led_button_led", "gpio_exti6" ]                         # PB6
17: [ "button", "output", "led_button", "gpio_exti3" ]                             # PB3
18: [ "button", "output", "led_button_led", "gpio_exti15" ]                        # PA15
19: [ "button", "output", "led_button", "gpio_exti14" ]                            # PC14
20: [ "button", "output", "led_button_led", "gpio_exti3" ]                         # PA3
21: [ "button", "output", "led_button", "gpio_exti2" ]                             # PA2
```

```json
{
  "0": {
    "type": "button",
    "active_level": 0,
    "long_press": 0
  },
  "1": {
    "type": "output",
    "active_level": 0
  },
  "2": {
    "type": "led_button",
    "active_level": 0
  },
  "3": {
    "type": "led_button_led"
  },
  "4": {
    "type": "counter",
    "active_level": 0,
    "tick": 1000
  }
}
```

</details>



Просмотр портов в реестре. Программа `com0com` нужна для того чтобы сделать петлю.


## Модульная система

Модули могут работать как одиночно, в этом случае они подключаются по Ethernet, так и связываться по шине CAN, если в
данном месте модулей нужно более одного.

![](can_modules.svg)

## Распайка компонентов портов

[см.](gpio_pic/readme.md)

## Реализация на stm32qubeMX

[stm32qubeMX](stm32qube/readme.md)

