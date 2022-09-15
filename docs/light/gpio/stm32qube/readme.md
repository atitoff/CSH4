# Реализация на stm32qubeMX

<details><summary><b>Uart1</b></summary>

![](uart1/img.png)

![](uart1/img_1.png)

```c
uint8_t UART1_rxBuffer[4] = {0};

int main(void) {
    // ...
    HAL_UART_Receive_DMA(&huart1, UART1_rxBuffer, 4);
    // ...
}

void HAL_UART_RxCpltCallback(UART_HandleTypeDef *huart)
{   
    // add to queue
    HAL_UART_Receive_DMA(&huart1, UART1_rxBuffer, 4);
}
```

</details>


