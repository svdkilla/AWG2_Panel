# API администраторов, нод и брендинга

## Администраторы

```bash
curl -b cookie.txt http://<host>:51351/api/admins

curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X POST http://<host>:51351/api/admins \
  -d '{"username":"seller1","password":"<strong-password>","role":"seller"}'

curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X PATCH http://<host>:51351/api/admins/3 \
  -d '{"password":"<new-strong-password>"}'

curl -b cookie.txt -X DELETE http://<host>:51351/api/admins/3
```

## Ноды

```bash
curl -b cookie.txt http://<host>:51351/api/nodes

curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X POST http://<host>:51351/api/nodes \
  -d '{
    "code":"nl",
    "name":"Netherlands",
    "country":"NL",
    "base_url":"http://203.0.113.10:51351",
    "token":"<node-agent-token>",
    "enabled":true,
    "is_local":false
  }'
```

Обновить, проверить, импортировать и удалить:

```bash
curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X PATCH http://<host>:51351/api/nodes/2 \
  -d '{"enabled":true,"name":"Netherlands 1"}'

curl -b cookie.txt -X POST http://<host>:51351/api/nodes/2/probe
curl -b cookie.txt -X POST http://<host>:51351/api/nodes/2/import
curl -b cookie.txt -X DELETE http://<host>:51351/api/nodes/2
```

## Брендинг

```bash
curl -b cookie.txt http://<host>:51351/api/settings/branding

curl -b cookie.txt \
  -H "Content-Type: application/json" \
  -X PATCH http://<host>:51351/api/settings/branding \
  -d '{
    "public_name":"MyVPN",
    "public_subtitle":"Доступ к VPN",
    "subscription_title_template":"Подписка {username}",
    "config_filename_prefix":"myvpn",
    "config_description_template":"{brand} {device}"
  }'
```
