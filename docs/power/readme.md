# Электропитание

Проще и дешевле всего применить хорошо зарекомендовавшие себя модули заряда и контроля батарей
от солнечных систем электропитания.

Например такой [модуль](https://powmr.com/solar-charge-controller/current/40amps-mppt/powmr-40a-mppt-solar-charge-controller-12v-24v-36v-48v-auto-solar-regulator-with-lcd-display-mppt-40a/)
более чем достаточен. Можно даже [попроще](https://powmr.com/solar-charge-controller/series-en/solar-laderegler-pwm-30a-40a-50a-60a-80a-automat-solar-controller-12v-24v-36v-48v-pv100v-lithiumbatterien-ternare-lithiumbatterien-lithiumeisenphosphat-usw./)

![](solar.svg)

Лучше всего применить LiFePO4 аккумуляторы.

|  | | 14s | 15s |
| ---- | ---- | ---- | ---- |
| Recovery Charging Voltage | Напряжение восстановления заряда | 47,6 | 51 |
| Constant Charging Voltage | Постоянное напряжение зарядки (буферный режим) | 50,4 | 54 |
| Low Voltage Disconnection | Отключение при низком напряжении | 39,2 | 42 |
| Low Voltage Reconnection | Повторное подключение | 44,8 | 48 |
| Load Over-Voltage Disconnection | Отключение от перенапряжения нагрузки | 51,8 | 55,5 |
| Load Over-Voltage Re-connection | Повторное подключение перенапряжения нагрузки | 50,4 | 54 |