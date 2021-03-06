---
layout: post
title: Тяжёлая артиллерия или отладка Arduino сетчей для МК Cortex
---

Порой бывают моменты когда кажется, что ты перепробовал уже всё, но код не работает. 
С грустью вспоминаешь о Кейле с его отладчиком. 
В очередной раз шлёшь лучи поноса программистам разрабатывающим Arduino IDE за то что она такая кривая и не имеет отладчика.
  
Но выход есть! Да, он немного корявый и тем не менее.
Идея состоит в том чтобы запустить таки отладку скетча пускай и не в Arduino.
  
Для работы нам понадобятся:
1. Тестовая версия [**Keil MDK-ARM**](https://www.keil.com/demo/eval/arm.htm#/DOWNLOAD).
2. Отладчик [**Jlink**](http://ali.ski/DCp-ZJ) или [**STlink**](http://ali.ski/l6lcZ). Рекомендуется иметь сразу оба если мы хотим комфортно работать с nrf из разных сред.
3. Arduno скетч в формате elf.
  
Итак по порядку.
  
Программа Keil MDK-ARM стоит вполне себе солидных денег. Но во первых ищущий как известно всегда найдёт искомое, 
а во вторых нам достаточно триального бесплатного режима (компиляция ограничена 32 килобайтами). 
Но нам то компилировать не надо, нам достаточно отладки. Поэтому скачаваем его и устанавливаем.
  
Считаем что дрова для отладчиков уже установлены.

Наши действия такие:
1. Запускаем Arduino IDE.
2. Выставляем необходимый уровень сборки с отладочной информацией. 
Если кодим под STM32, то в файле
C:\Users\\*указать_своего_пользователя*\Documents\Arduino\hardware\Arduino_STM32\STM32F1\boards.txt 
вносим следующие изменения:
  
Было:
genericSTM32F103C.menu.opt.ogstd.build.flags.optimize=-Og
  
Стало:
genericSTM32F103C.menu.opt.ogstd.build.flags.optimize=-Og **-gdwarf-2**
  
Далее выбираем в меню:

![Выбор режима отладки](/images/stm32_debug.JPG)

Если же мы кодим nrf5, то данного пункта в меню нет. 
Поэтому нам надо временно добавить пару флагов отладки в файл - 
C:\Users\\*указать_своего_пользователя*\AppData\Local\Arduino15\packages\MySensors\hardware\nRF5\0.3.0\board.txt

Было:
MyBoard_nRF52832.build.extra_flags=-DNRF52 -DMYBOARDNRF5 -I{build.path}
  
Надо сделать:
MyBoard_nRF52832.build.extra_flags=**-Og -gdwarf-2** -DNRF52 -DMYBOARDNRF5 -I{build.path}
  
Теперь в наш исполнимый файл (файл с расширением **elf**) будет включена отладочная информация.
  
3. Собираем скетч и грузим его в МК.
    
4. Находим путь сборки проекта.
  
![](/images/debug_build_path.JPG)
  
5. Запускаем Keil MDK. И далее по картинкам.
  
Если у нас был открыт проект, то закрываем его. 

![](/images/debug_close_project.JPG)

Начинаем новый проект. 

![](/images/debug_new_project.JPG)

Выбираем тип МК. 
Если у нас его нет, то необходимо его доустановить. 

![](/images/debug_select_MCU.JPG)

Выбираем подключаемые компоненты. Можно ничего не выбирать, а сразу жать - **OK**.

![](/images/debug_env_OK.JPG)

Идём в настройки опций проекта. 

![](/images/debug_options.JPG)

На закладке **Debug** выбираем тип отладчика. И убираем галку с пункта **Load Application at Startup**.

![](/images/debug_select_debugger.JPG)
![](/images/debug_unselect_load_app.JPG)

Переходим на закладку **Utilities** и убираем галку с **Update Target Before Debugging**.

![](/images/debug_utilities.JPG)

Далее переключаемся снова на закладку **Debug** и жмём кнопку **Settings**.

![](/images/debug_debug_settings.JPG)

Преключаемся на закладку **Flash Download** и если поле **Programming Algorithm** пустое, то жмём кнопку **Add**.

![](/images/debug_flash_download.JPG)

В появившемся списке выбираем свой МК, жмём **Add**.

![](/images/debug_add_flash_alg.JPG)

Далее нажимаем **OK**, затем опять **OK**.
И наконец можно запускать отладчик. Жмём кнопку его запуска.

![](/images/debug_start_debug_session.JPG)

Далее Кейл нам ругнётся на ограничение по размеру, нажимаем **OK**.

![](/images/debug_eval_mode.JPG)

И вот мы уже в отладчике, осталось только загрузить исполняемый файл.
Щёлкаем по коммандной строке внизу. 

![](/images/debug_load_elf.JPG)

И вбиваем команду:
**load** *свой путь до файла .elf*

Жмём кнопку Enter.

ВСЁ!!! :) 

 Можно приступать к отладке.

![](/images/debug_end2.JPG)



И напоследок. 
Одна из самых важных вещей даруемая нам при отладке, это возможность смотреть и **править** регистры МК.

![](/images/debug_add_regs_windows.JPG)
![](/images/debug_windows_GPIO.JPG)

Данная статья написана исключительно для [канала https://t.me/mysensors](https://t.me/mysensors) и [группы https://t.me/mysensors_rus](https://t.me/mysensors_rus).
Публикация данной статьи на других ресурсах разрешается только при указании [первоисточника](mysensors-rus/mysensors-rus.github.io)!

Dab0G.
