# Публичный и Agent API

## Публичный API подписки

Токен передаётся в URL и заменяет авторизацию.

Получить данные:

```bash
curl http://<host>:51351/api/portal/<token>
```

Управление устройствами:

```bash
curl -H "Content-Type: application/json" \
  -X POST http://<host>:51351/api/portal/<token>/devices \
  -d '{"name":"iPhone","node_id":2}'

curl -H "Content-Type: application/json" \
  -X PATCH http://<host>:51351/api/portal/<token>/devices/55 \
  -d '{"name":"iPhone 15"}'

curl -X DELETE http://<host>:51351/api/portal/<token>/devices/55
```

Получить конфигурацию:

```bash
curl -OJ http://<host>:51351/api/portal/<token>/devices/55/config
curl http://<host>:51351/api/portal/<token>/devices/55/key
curl -o qr.png http://<host>:51351/api/portal/<token>/devices/55/qr.png
curl -o qr-native.png http://<host>:51351/api/portal/<token>/devices/55/qr-native.png
```

## Agent API

Agent API используется главной панелью. Авторизация:

```text
X-Node-Token: <NODE_AGENT_TOKEN>
```

Также поддерживается:

```text
Authorization: Bearer <NODE_AGENT_TOKEN>
```

Проверка и экспорт:

```bash
curl -H "X-Node-Token: <token>" \
  http://<node-host>:51351/api/node-agent/info

curl -H "X-Node-Token: <token>" \
  http://<node-host>:51351/api/node-agent/export

curl -H "X-Node-Token: <token>" \
  http://<node-host>:51351/api/node-agent/devices
```

Создать пользователя и устройство:

```bash
curl -H "X-Node-Token: <token>" \
  -H "Content-Type: application/json" \
  -X POST http://<node-host>:51351/api/node-agent/users \
  -d '{
    "username":"client1",
    "status":"active",
    "expires_at":"2027-08-27T00:00:00+03:00",
    "device_limit":5,
    "traffic_limit_gb":250
  }'

curl -H "X-Node-Token: <token>" \
  -H "Content-Type: application/json" \
  -X POST http://<node-host>:51351/api/node-agent/users/10/devices \
  -d '{"name":"iPhone"}'
```

Скачать конфиг с ноды:

```bash
curl -H "X-Node-Token: <token>" -OJ \
  http://<node-host>:51351/api/node-agent/devices/55/config
```

Обычно эти маршруты вызывает главная панель. Ручные запросы нужны при первичной проверке ноды и диагностике связи.
