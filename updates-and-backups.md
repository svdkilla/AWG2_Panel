# Обновление и резервные копии

Перед обновлением сохраните как встроенный бэкап, так и полный архив каталога панели.

## Встроенный бэкап

В интерфейсе владельца откройте «Бэкапы» и нажмите «Создать». Через API:

```bash
curl -b cookie.txt -X POST http://<host>:51351/api/backups
```

Архив сохраняется в:

```text
/opt/xconnect-awg-panel/data/backups
```

В него входят panel.sqlite3, локальный awg0.conf и meta.json.

Бэкап главной панели не скачивает AWG-конфиги удалённых нод. Создавайте резервные копии на каждой ноде отдельно.

## Полный архив перед обновлением

```bash
cd /opt
tar -czf xconnect-awg-panel-before-update-$(date +%Y%m%d-%H%M%S).tar.gz \
  xconnect-awg-panel
```

## Обновление

Загрузите новую сборку в /opt/xconnect-awg-panel, затем выполните:

```bash
cd /opt/xconnect-awg-panel
chmod +x install.sh
./install.sh
```

Скрипт пересобирает image и контейнер, сохраняя data/panel.sqlite3 и data/panel.env.

## Проверка после обновления

```bash
docker ps --filter name=xconnect-awg-panel
docker logs --tail=100 xconnect-awg-panel
```

## Восстановление встроенного бэкапа

```bash
curl -b cookie.txt -X POST \
  http://<host>:51351/api/backups/<backup-name>.tar.gz/restore
```

Панель заменит SQLite-базу и применит локальный AWG-конфиг через awg syncconf.
