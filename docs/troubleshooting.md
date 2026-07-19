# Диагностика

## Панель не открывается

```bash
docker ps --filter name=xconnect-awg-panel
docker logs --tail=100 xconnect-awg-panel
ss -tulpn | grep 51351
```

Проверьте firewall сервера и сетевые правила провайдера. Если используется reverse proxy, отдельно проверьте его upstream и сертификат.

## Пользователь создан, но VPN не подключается

```bash
docker ps --filter name=amnezia-awg2
docker exec -it amnezia-awg2 sh -lc 'awg show awg0'
docker logs --tail=100 xconnect-awg-panel
```

Частые причины:

- закрыт UDP-порт AWG;
- PUBLIC_HOST содержит старый IP;
- пользователь имеет статус expired или blocked;
- превышен лимит трафика;
- устройство удалено;
- нода недоступна с главной панели;
- в base_url пропущен порт;
- NODE_AGENT_TOKEN на серверах не совпадает.

## Нода не отвечает

С главного сервера:

```bash
curl -H "X-Node-Token: <token>" \
  http://<node-ip>:51351/api/node-agent/info
```

На ноде:

```bash
docker logs --tail=100 xconnect-awg-panel
grep '^NODE_AGENT_TOKEN=' /opt/xconnect-awg-panel/data/panel.env
```

## После смены IP

```bash
cd /opt/xconnect-awg-panel
nano data/panel.env
./install.sh
```

Измените PUBLIC_HOST, а для удалённой ноды также обновите base_url в главной панели. Клиентам со старым IP в endpoint потребуется новый конфиг.

## После импорта

Проверьте разрешённые серверы, список устройств и конфигурацию каждой страны. Старые устройства не должны менять ключи без причины.
