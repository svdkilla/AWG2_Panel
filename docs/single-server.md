# Панель и AWG на одном сервере

Локальная схема подходит, когда панель управляет одним AWG-сервером и отдельные страны не требуются.

## Подготовка

1. Установите AmneziaWG 2.0.
2. Убедитесь, что контейнер amnezia-awg2 запущен.
3. Скопируйте сборку панели в /opt/xconnect-awg-panel.

```bash
docker ps --filter name=amnezia-awg2
```

## Запуск установки

```bash
cd /opt/xconnect-awg-panel
chmod +x install.sh
PUBLIC_HOST=<server-ip> PORT=51351 ./install.sh
```

После завершения скрипт покажет адрес панели и имя первого администратора. Пароль сохраняется в data/panel.env:

```bash
grep '^ADMIN_PASSWORD=' /opt/xconnect-awg-panel/data/panel.env
```

Если база уже существует, повторный запуск install.sh не заменяет текущие учётные данные.

## Проверка

```bash
docker ps --filter name=xconnect-awg-panel
docker logs --tail=100 xconnect-awg-panel
```

Откройте:

```text
http://<server-ip>:51351
```

## Что происходит при создании устройства

1. Панель генерирует ключи.
2. Сохраняет устройство и peer в SQLite.
3. Пересобирает awg0.conf.
4. Применяет изменения через awg syncconf.

Peer-блоки, созданные вручную и не помеченные как XConnectPanel = managed, должны сохраняться при пересборке.
