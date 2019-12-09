![Logo](admin/mihome.png)
# mihome Gateway


## Описание
        
  Эта модификация  позволяет управлять кондиционером подключенным к ioBroker с помощью acpartner.v3 (KTBL11LM), (возможно будет работать и с версией v2, но у меня нет устройства для проверки, если кто-либо испытает - сообщите).
  
  При разработке данного адаптера использовался адаптер iobroker.mihome версии 1.2.9, поэтому я выражаю огромную благодарность всем авторам принимавшим участие в этой работе: https://github.com/ioBroker/ioBroker.mihome/graphs/contributors.
  
  Основной момент заключается в том что по-видимому китайские облака Xiaomi и Aqara используют разные команды в сетевом протоколе. Для Aqara есть некоторая документация - http://docs.opencloud.aqara.com/en/development/gateway-LAN-communication/#air-conditioning-controller. Для Xiaomi подобной документации в широком доступе не существует. Подключив шлюз-acpartner к облаку Aqara я получил обновление firmware, которое позволило использовать команды управления кондиционером, описанные в приведенной выше ссылке. Побочным эффектом является то что похоже в прошивке от Aqara нет протокола miio, по крайней мере acpartner больше не виден для команды miio-discovery.
  
  Некоторую сложность может доставить процесс включения LAN доступа и получения GATEWAY KEY - процесс описан ниже.
  
  Для начала использования:
  - установите на смартфон приложение Aqara Home (https://play.google.com/store/apps/details?id=com.lumiunited.aqarahome),
  - зарегестрируйтесь в приложении Aqara Home,
  - выберите в настройках регион "Материковый китай",
  - добавьте acpartner в приложение Aqara Home,
  - обновите прошивку acpartner (нажмите на иконку кодиционера, затем три точки в правом верхнем углу, затем нажмите самый нижний пункт     "Версия ПО"), в результате на acpartner будет установлена прошивка Aqara (при использовании приложения MiHome была от Xiaomi),
  - зарегестрируйтесь на сайте https://opencloud.aqara.cn/ с тем же паролем и логином как и в приложении Aqara Home (подтверждение     регистрации может занять некоторое время, у меня было около 6 часов),
  - войдите в консоль https://opencloud.aqara.cn/console/
  - создайте приложение на вкладке https://opencloud.aqara.cn/console/app-management с типом "Device access" (в необходимости данного пункта я не уверен (потому что сделал его пока разбирался), поэтому можно попробовать его пропустить),
  - затем перейдите в консоль https://opencloud.aqara.cn/console и выберите Gateway LAN слева, заполните поля "Aqara account" и "Password" и нажмите кнопку Submit - вы увидите свой Air Conditioning Controller и кнопку включения сетевого протокола, нажав на которую вы разрешите LAN доступ и увидите ключ сети, который необходим для настройки адаптера в ioBroker.
  - установите адаптер с этой страницы, в настройках введите ключ полученный выше.  
  
  По отношению к официальной версии адаптера были модифицированы следующие файлы:
  - main.js
  - Hub.js
  - Gateway.js
  - devices.js
  - THSensor.js  

### Поддерживаемые устройства:
- Все доступные на момент версии 1.2.9 и поддержка управления кондиционером через acpartner.v3
- gateway -           Xiaomi RGB Gateway
- sensor_ht -         Xiaomi Temperature/Humidity
- weather.v1 -        Xiaomi Temperature/Humidity/Pressure
- switch -            Xiaomi Wireless Switch
- sensor_switch.aq2 - Xiaomi Aqara Wireless Switch Sensor
- sensor_switch.aq3 - Xiaomi Aqara Wireless Switch Sensor
- plug -              Xiaomi Smart Plug
- 86plug -            Xiaomi Smart Wall Plug
- 86sw2 -             Xiaomi Wireless Dual Wall Switch
- 86sw1 -             Xiaomi Wireless Single Wall Switch
- natgas -            Xiaomi Mijia Honeywell Gas Alarm Detector
- smoke -             Xiaomi Mijia Honeywell Fire Alarm Detector
- ctrl_ln1 -          Xiaomi Aqara 86 Fire Wall Switch One Button
- ctrl_ln1.aq1 -      Xiaomi Aqara Wall Switch LN
- ctrl_ln2 -          Xiaomi 86 zero fire wall switch double key
- ctrl_ln2.aq1 -      Xiaomi Aqara Wall Switch LN double key
- ctrl_neutral2 -     Xiaomi Wired Dual Wall Switch
- ctrl_neutral1 -     Xiaomi Wired Single Wall Switch
- cube -              Xiaomi Cube
- sensor_cube.aqgl01 - Xiaomi Cube
- magnet -            Xiaomi Door Sensor
- sensor_magnet.aq2 - Xiaomi Aqara Door Sensor
- curtain -           Xiaomi Aqara Smart Curtain
- motion -            Xiaomi Motion Sensor
- sensor_motion.aq2 - Xiaomi Aqara Motion Sensor
- sensor_wleak.aq1 -  Xiaomi Aqara water sensor
- ctrl_ln2.aq1 -      Xiaomi Aqara Wall Switch LN (Double)
- remote.b286acn01 -  Xiaomi Aqara Wireless Remote Switch (Double Rocker)
- remote.b1acn01 -    Xiaomi Aqara Wireless Remote Switch
- vibration -         Xiaomi vibration Sensor
- wleak1 -            Xiaomi Aqara Water Sensor
- lock_aq1 -          Xiaomi Lock

## Changelog
### 1.2.9 (2019-11-15)
* (Diginix) Fixed pressure range and values of Aqara weather sensor


Copyright (c) 2017-2019 bluefox <dogafox@gmail.com>
