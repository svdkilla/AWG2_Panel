# API пользователей и устройств

Все запросы на этой странице требуют -b cookie.txt.

## Пользователи

Список:

```bash
curl -b cookie.txt http://<host>:51351/api/users
```

Создание:

```bash
curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X POST http://<host>:51351/api/users \
  -d '{
    "username": "client1",
    "status": "active",
    "expires_at": "2027-08-27T00:00:00+03:00",
    "device_limit": 5,
    "traffic_limit_gb": 250,
    "email": "client@example.com",
    "comment": "Оплата до августа",
    "node_ids": [1, 3]
  }'
```

ПолеТипОписаниеusernamestringобязательно при созданииstatusstringactive, expired или blockedexpires_atstring/nullISO 8601, допускается +03:00device_limitnumber0 — без ограниченияtraffic_limit_gbnumber0 — без ограниченияtelegram_idstringнеобязательный контактemailstringнеобязательный контактcommentstringвнутренний комментарийnode_idsarray/number/nullсписок; 0 или отсутствие — все нодыserver_idsarray/number/nullалиас node_idsnode_idnumberодна нодаserver_idnumberалиас node_id

Получить, изменить и удалить:

```bash
curl -b cookie.txt http://<host>:51351/api/users/10

curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X PATCH http://<host>:51351/api/users/10 \
  -d '{"status":"active","node_ids":[1,2,4]}'

curl -b cookie.txt -X DELETE http://<host>:51351/api/users/10
```

## Устройства

Создать:

```bash
curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X POST http://<host>:51351/api/users/10/devices \
  -d '{"name":"iPhone","node_id":2}'
```

Без node_id устройство создаётся на всех разрешённых нодах пользователя.

Переименовать и удалить:

```bash
curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X PATCH http://<host>:51351/api/devices/55 \
  -d '{"name":"MacBook"}'

curl -b cookie.txt -X DELETE http://<host>:51351/api/devices/55
```

Получить конфигурацию:

```bash
curl -b cookie.txt -OJ http://<host>:51351/api/devices/55/config
curl -b cookie.txt http://<host>:51351/api/devices/55/key
curl -b cookie.txt -o qr.png http://<host>:51351/api/devices/55/qr.png
curl -b cookie.txt -o qr.svg http://<host>:51351/api/devices/55/qr.svg
curl -b cookie.txt -o qr-native.png http://<host>:51351/api/devices/55/qr-native.png
curl -b cookie.txt -o qr-native.svg http://<host>:51351/api/devices/55/qr-native.svg
```
