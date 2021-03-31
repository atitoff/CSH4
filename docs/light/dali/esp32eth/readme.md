# Интерфейс DALI на базе ESP32ETH

### Принцип кодирования

Сначала преобразуем в манчестерский код, а потом сгенерируем последовательность для RMT.

The RMT is ESP32-specific and allows generation of accurate digital pulses with 12.5ns resolution.

Рассчитываем делитель

![](tact_rmt.png)

Генерим последовательность как в примере с декодированием 10110