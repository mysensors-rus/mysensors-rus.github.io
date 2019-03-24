---
layout: post
title: nrf52840 Первые шаги
---

nrf52840 по ["даташиту"](https://www.nordicsemi.com/DocLib/Content/Product_Spec/nRF52840/latest/keyfeatures_html5) имеет очень много вкусгых плюшек.

Для изучения я заказал модули E73-2G4M08S1C. Перед началом их программирования необходимо произвести процедуру "recover" - некого восстановнения, не понятно правда от чего ...

Ну да ладно. Запускаем nRFgo Studio и получаем облом - студия чип **не** видит.

![nRFgo Studio](/images/nrf52840_1.JPG "Облом 1")

Кстати процедура восстановления проводиться Jlink-ом, в дальнейшем после "восстановления" можно его программировать и Stlink-ом.

Попытка восстановления программой nRF Connect c модулем Programmer так же ни к чему не привела - чип не увиделся :(

![nRF Connect](/images/nrf52840_2.JPG "nRF Connect")

![nRF Connect](/images/nrf52840_3.JPG "nRF Connect облом 2")

Но необъятные пучины интернета подсказали ещё один способ.

[nRF5x-Command-Line-Tools](https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF5-Command-Line-Tools)

Скачиваем, устанавливаем (со всеми драйверами), запускаем:

>**nrfjprog -f NRF52 --recover**

>Recovering device. This operation might take 30s.

>Erasing user code and UICR flash areas.

**И о чудо! Чип восстановился! :)**

После этой процедуры уже можно очистить чип в nRFgo Studio.

![nRFgo Studio](/images/nrf52840_4.JPG "nRFgo Studio")

После этого модуль прекрасно видиться и шьётся из под Arduino IDE и замечательно работает в MySensors.

Продолжение следует ...
