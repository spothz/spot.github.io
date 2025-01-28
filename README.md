# https://spothz.github.io/spot.github.io/
---
# 1. Простое использование UCI openwrt.


UCI (Unified Configuration Interface) — это инструмент для управления конфигурацией в OpenWrt. Он позволяет изменять параметры системы через командную строку, обеспечивая удобство работы со сложными конфигурационными файлами.

### Основные команды UCI:
1. **Просмотр текущей конфигурации**:

uci show [путь к конфигурации]
Например:

	uci show network

Покажет все настройки раздела `network`.

2. **Изменение параметров**:
Чтобы изменить параметр, используйте команду:

uci set [путь к параметру]=[новое значение]
Например, чтобы задать IP-адрес на интерфейсе LAN:

uci set network.lan.ipaddr='192.168.1.100'
Прото достаточно взглянуть на uci show network и там будет все названия опций.

3. **Добавление новых секций или параметров**:

uci add [имя файла] [тип секции]
uci set [путь к параметру]=[значение]
Например, для добавления нового правила firewall:



uci add firewall rule
uci set firewall.@rule[-1].name='Allow-SSH'
uci set firewall.@rule[-1].src='wan'
uci set firewall.@rule[-1].dest_port='22'
uci set firewall.@rule[-1].target='ACCEPT'

4. **Удаление секции или параметра**:

uci delete [путь к параметру или секции]
Например:

uci delete network.lan.dns

5. **Сохранение изменений и их применение**:
После внесения изменений сохраните их с помощью:

uci commit [имя файла]
Например:

uci commit network
Чтобы изменения вступили в силу, иногда нужно перезапустить сервис:
/etc/init.d/network restart


### Примеры использования:
1. **Изменение имени хоста**:

uci set system.@system[0].hostname='MyOpenWrt'
uci commit system
/etc/init.d/system reload

2. **Настройка Wi-Fi**:
Включение Wi-Fi:

uci set wireless.@wifi-device[0].disabled='0'
uci commit wireless
/etc/init.d/network restart

Изменение SSID:

uci set wireless.@wifi-iface[0].ssid='MyNewSSID'
uci commit wireless
/etc/init.d/network restart


### Подсказки:
- **@** обозначает первую найденную секцию определенного типа. `@wifi-iface[0]` — первая секция типа `wifi-iface`.
- **[-1]** указывает на последнюю добавленную секцию.

Надеюсь, эти примеры помогут вам понять основы работы с UCI в OpenWrt.




