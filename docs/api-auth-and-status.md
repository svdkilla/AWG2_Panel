# Авторизация и состояние

Админское API использует cookie-сессию.

## Вход

```bash
curl -c cookie.txt \
  -H "Content-Type: application/json" \
  -X POST http://<host>:51351/api/login \
  -d '{"username":"admin","password":"<password>"}'
```

Успешный ответ:

```json
{"ok": true}
```

## Текущая сессия

```bash
curl -b cookie.txt http://<host>:51351/api/me
```

## Выход

```bash
curl -b cookie.txt -X POST http://<host>:51351/api/logout
```

## Сводка и состояние

```bash
curl -b cookie.txt http://<host>:51351/api/overview
curl -b cookie.txt http://<host>:51351/api/status
```

/api/overview возвращает пользователей, счётчики, ноды и состояние фоновой синхронизации. /api/status содержит системные и AWG-метрики.
