---
layout: post
title: Итак поехали!!! STM32
---

У меня есть несколько плат на МК STM32. Я во время отладки загружаю прошивку ST-Link-ом. Но вот беда он жёстко пишет прошивку с адреса 0x8000000, а если у меня уже прошит загрузчик, то всё, прощай?! Поэтому первым делом добавляем возможность выбора адреса загрузки прошивки во флэш МК, и чтобы программа запустилась - сдвиг таблицы прерываний.

Коммит в (https://github.com/mysensors-rus/Arduino_STM32/commit/740771a1dfd1985e84f533997809fb41c389d134 "mysensors-rus/Arduino_STM32")


На этом пока всё. :)
