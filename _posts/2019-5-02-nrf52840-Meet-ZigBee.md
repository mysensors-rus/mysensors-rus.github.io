---
layout: post
title: nrf52840 Знакомство с ZigBee
---

Для начала работы нам понадобиться следующее ПО:
1. [Segger Embedded Studio](https://www.segger.com/downloads/embedded-studio), для разработки, компиляции бинарников и дебага - всё в одном (бесплатно для нордиковых устройств - лицензию получает само автоматом).
2. [Zigbee SDK](https://www.nordicsemi.com/?sc_itemid=%7B55A66FBE-42A1-4ABE-A8F4-17F8D86DD41A%7D), текущаяя версия - 3.  Ставить не надо, просто распаковывается и всё.

Из железа понадобиться программатор J-link, например [такой](https://ru.aliexpress.com/item/High-Speed-J-Link-JLink-V8-USB-ARM-JTAG-Emulator-Debugger-J-Link-V8-Emulator/32908271509.html?spm=a2g0v.search0104.3.190.771f11f2cO1rGp&ws_ab_test=searchweb0_0,searchweb201602_9_10065_10068_10547_319_317_10696_453_10084_454_10083_10618_10304_10307_10820_10301_537_536_10843_10059_10884_10889_10887_321_322_10103_10914_10911,searchweb201603_52,ppcSwitch_0&algo_expid=b76085ff-164b-4944-a65a-a9ae447c25bf-27&algo_pvid=b76085ff-164b-4944-a65a-a9ae447c25bf&transAbTest=ae803_5).
