# Главный сервер и VPN-ноды

В мультисерверной схеме главная панель хранит общую базу, а каждая VPN-нода применяет команды через agent API.

## Архитектура

На каждой ноде должны работать:

- AmneziaWG 2.0;
- контейнер xconnect-awg-panel;
- уникальный NODE_AGENT_TOKEN;
- доступный с главного сервера TCP-порт панели.

Главный сервер также может быть локальной VPN-нодой.

## Установка ноды

```bash
cd /opt/xconnect-awg-panel
chmod +x install.sh
PUBLIC_HOST=<node-ip> \
PORT=51351 \
NODE_CODE=<code> \
NODE_NAME="<name>" \
NODE_COUNTRY="<country>" \
./install.sh
```

Пример:

```bash
PUBLIC_HOST=203.0.113.10 \
PORT=51351 \
NODE_CODE=nl \
NODE_NAME="Netherlands" \
NODE_COUNTRY="NL" \
./install.sh
```

Получить токен:

```bash
grep '^NODE_AGENT_TOKEN=' /opt/xconnect-awg-panel/data/panel.env
```

## Проверка agent API

С главного сервера выполните:

```bash
curl -H "X-Node-Token: <node-token>" \
  http://<node-ip>:51351/api/node-agent/info
```

Исправная нода возвращает JSON с "ok": true.

## Подключение в главной панели

1. Откройте «Серверы» и добавьте ноду.
2. Укажите короткий код, название и страну.
3. В base_url внесите полный адрес с портом, например http://203.0.113.10:51351.
4. Вставьте NODE_AGENT_TOKEN.
5. Для ноды на главном сервере включите is_local.
6. Сохраните и нажмите «Проверить».

Если node_ids не передан, пуст или равен 0, пользователь получает доступ ко всем активным нодам. Явный массив ограничивает доступ указанными серверами.
