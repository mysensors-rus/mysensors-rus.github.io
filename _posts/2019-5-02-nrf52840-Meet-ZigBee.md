---
layout: post
title: nrf52840 Знакомство с ZigBee
---

  Для начала работы нам понадобиться следующее ПО:
  1. [Segger Embedded Studio](https://www.segger.com/downloads/embedded-studio), для разработки, компиляции бинарников и дебага - всё в одном (бесплатно для нордиковых устройств - лицензию получает само автоматом).
  2. [Zigbee SDK](https://www.nordicsemi.com/?sc_itemid=%7B55A66FBE-42A1-4ABE-A8F4-17F8D86DD41A%7D), текущаяя версия - 3.  Ставить не надо, просто распаковывается и всё.
  
  Модули [E73-2G4M08S1C](http://ali.ski/Sn8BHa) от CDEBYTE требуют [разлочки](https://mysensors-rus.github.io/nrf52840-The-first-steps/). 

  Из железа понадобиться программатор J-link, например [такой](http://ali.ski/DCp-ZJ).

  После установки Segger Embedded Studio она спросит не хотите ли вы активировать бесплатный ключ для Nordic устройств, щёлкаем что мол хотим, заполняем поля, указываем почту. Затем из почты копируем ключ и вводим его в предложенное окно, щёлкаем - активировать и всё.

  Если мы хотим посмотреть как и какие пакеты шастают по меш сети, то можно прошить свой модуль в [сниффер](https://github.com/NordicSemiconductor/nRF-Sniffer-for-802.15.4). Далее действуем строго по инструкции.
 
  
  
