# Ежедневные команды

## Состояние и логи

```bash
docker ps --filter name=xconnect-awg-panel
docker logs -f xconnect-awg-panel
```

## Перезапуск панели

```bash
docker restart xconnect-awg-panel
```

## Переустановка с сохранением данных

```bash
cd /opt/xconnect-awg-panel
./install.sh
```

## Секреты первого запуска

```bash
grep '^ADMIN_PASSWORD=' /opt/xconnect-awg-panel/data/panel.env
grep '^NODE_AGENT_TOKEN=' /opt/xconnect-awg-panel/data/panel.env
```

Не отправляйте вывод этих команд в публичные чаты и тикеты.

## Состояние AWG

```bash
docker exec -it amnezia-awg2 sh -lc 'awg show awg0'
```

## Полный архив каталога

```bash
cd /opt
tar -czf xconnect-awg-panel-full-$(date +%Y%m%d-%H%M%S).tar.gz \
  xconnect-awg-panel
```

## Проверка ноды

```bash
curl -H "X-Node-Token: <token>" \
  http://<node-ip>:51351/api/node-agent/info
```
