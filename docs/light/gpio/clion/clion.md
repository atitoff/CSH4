# Настройка CLion

## Импортируем проект STM32CubeMX

![img.png](img.png)

![img_1.png](img_1.png)

![img_2.png](img_2.png)

Закрываем не обращая внимания.

![img_3.png](img_3.png)

## Настраиваем дебаггер

Menu -> Run -> Edit Configuration

![img_4.png](img_4.png)

Распаковываем, например, в `D:\Alex\dev\STM32CubeIDE`
[архив](plugins.7z)

Удаляем все конфигурации и создаем

![img_5.png](img_5.png)


![img_7.png](img_7.png)


GDB Server:
```
D:\Alex\dev\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.stlink-gdb-server.win32_2.0.300.202203231527\tools\bin\ST-LINK_gdbserver.exe
```
GDB Server args:
```
-p 61234 -l 1 -d -s -m 0 -k -cp D:\Alex\dev\STM32CubeIDE\plugins\com.st.stm32cube.ide.mcu.externaltools.cubeprogrammer.win32_2.0.300.202205161323\tools\bin
```