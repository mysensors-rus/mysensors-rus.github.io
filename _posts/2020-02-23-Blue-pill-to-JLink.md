---
layout: post
title: Делаем из BluePill пограмматор/отладчик JLink OB-STM32F103
---

Если нам нужен программатор **JLink**, а его нет и тратить деньги и время не охота, то можно попробовать его сделать самому.
Для этого нам понадобиться [**плата BluePill**](https://user-images.githubusercontent.com/48506975/75117838-3ac7cb00-5686-11ea-8e39-b6ef694aa237.png) на основе МК **STM32F103**, два резистора по 100 Ом, несколько кусочков провода, паяльник, припой с флюсом и прямые руки.

Припаиваем резистор 100 Ом между пинами PA5 и PA3, с пина PA3 получаем выход - SWCLK.
Припаиваем резистор 100 Ом между пинами PA7 и PA4, с пина PA4 получаем выход - SWDIO. Берём землю и 3.3В.

![Фото 1](https://user-images.githubusercontent.com/48506975/75135635-3980b780-56f3-11ea-95fc-7050e22b5911.jpg)

![Фото 2](https://user-images.githubusercontent.com/48506975/75135255-05f15d80-56f2-11ea-94a6-3fbb7df04e8a.jpg)

Заливаем [**прошивку**](https://github.com/mysensors-rus/mysensors-rus.github.io/files/4242110/OB_STM32F103.zip) отладчика JLINK в МК. Заливать можно как через внешний программатор (STLink, JLink и т.п.), так и через встроенный в МК загрузчик UART.

Далее надо установить [**драйвера JLink**](https://www.segger.com/downloads/jlink/#J-LinkSoftwareAndDocumentationPack) (если ещё не установлены).
Подключаем плату BluePill через USB к компу и видим появление нового устройства - JLink driver.
Затем надо запустить программу JLink.exe (из комплекта драйверов JLink. Устанавливается как правило по пути `C:\Program Files (x86)\SEGGER\JLink\` ) и командой `Exec SetSN=XXXXXXXX` (где X - любая цифра) задать серийный номер программатора.

![Серийный номер](https://user-images.githubusercontent.com/48506975/75135516-caa35e80-56f2-11ea-8b8b-9181fe4ec65e.JPG))

После этого прогамматор можно использовать по назначению :)
В том числе и для пограммирования/восстановления чипов nrf52(nrf51) в SEGGER Studio.

![Фото 3](https://user-images.githubusercontent.com/48506975/75134950-f7567680-56f0-11ea-8894-03bdb09643a4.jpg)

UPD 01.07.2020  Последние дрова JLink-а пытаются обновить наше йстройство и при этом его портят. Для устранения этой ситуации нужно залить более новую [**прошивку**](https://github.com/GCY/JLINK-ARM-OB/blob/master/2012%20version/jlink%20firmware.hex)

Данная статья написана для Телеграм канала [https://t.me/mysensors](https://t.me/mysensors) и группы [https://t.me/mysensors_rus](https://t.me/mysensors_rus).
Публикация данной статьи на других ресурсах разрешается только при указании [первоисточника](mysensors-rus.github.io)!

Dab0G.
