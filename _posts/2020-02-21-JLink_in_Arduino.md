---
layout: post
title: Добавляем нормальную поддержку JLink в Arduino IDE
---

  В данный момент (21.02.2020) в Arduino IDE поддержка JLink програаматора реализовано достаточно кривым методом, через Zadig. Да, после этого JLink начинает работать в Arduino IDE, но при этом он отваливается от всего остального (Keil, SEGGER Studio и т.п.) и это не есть хорошо.

  Попробуем исправить ситуацию. Для этого нам как всегда понадобиться ~~напильник и~~:

1. Скачать и установить с сайта Нордика пакет программ - [**nRF Command Line Tools.**](https://www.nordicsemi.com/Software-and-tools/Development-Tools/nRF-Command-Line-Tools). Добавить в переменную Path - Система->Дополнительные параметры системы->Переменные среды->Path->Изменить, путь к файлу nrfjprog.exe (если это уже не произошло при установке).

2. Добавить в конец файла **platform.txt** фреймворка [**arduino-nRF5**](https://github.com/sandeepmistry/arduino-nRF5) следующий текст:

``` 
#jlink upload
tools.jlink_upload.cmd=jlink_upload
tools.jlink_upload.cmd.windows=jlink_upload.bat
tools.jlink_upload.path={runtime.hardware.path}/0.6.0/tools/win
tools.jlink_upload.upload.params.verbose=-d
tools.jlink_upload.upload.params.quiet=n
tools.jlink_upload.upload.pattern="{path}/{cmd}" "{upload.target}" "{build.path}/{build.project_name}.hex"
```

3. В файле **boards.txt** того же флеймворка, для своей платы внести аналогичные изменения:

    Generic_nRF52840.upload.tool=***jlink_upload***  
    Generic_nRF52840.upload.protocol=jlink 
    Generic_nRF52840.upload.target=nrf52  
    Generic_nRF52840.upload.maximum_size=1048576

4. В директории фреймворка создаём папки arduino-nRF5/**tools/win**.
5. В директории /win/ создаём файл **jlink-upload.bat** со следующим содержанием:

    nrfjprog -f %1 --program %2 --chiperase -r
  
6. Данный пример приведён для Windows.
7. Запускаем Arduino IDE и радуемся. :)

Данная статья написана для Телеграм канала [https://t.me/mysensors](https://t.me/mysensors) и группы [https://t.me/mysensors_rus](https://t.me/mysensors_rus).
Публикация данной статьи на других ресурсах разрешается только при указании [первоисточника](mysensors-rus.github.io)!

Dab0G.
