# Параметры запуска

Панель читает настройки из data/panel.env и переменных окружения контейнера.

ПеременнаяПо умолчаниюНазначениеPORT51351внешний TCP-порт панелиPUBLIC_HOSTпервый IP сервераIP или домен в ссылках и клиентских конфигахPUBLIC_PORTзначение PORTпорт в публичных ссылкахPUBLIC_SCHEMEhttpсхема http или httpsAWG_CONTAINERamnezia-awg2имя AWG-контейнераAWG_CONF/opt/amnezia/awg/awg0.confконфиг внутри AWG-контейнераAWG_IFACEawg0имя AWG-интерфейсаADMIN_USERadminпервый owner-администраторADMIN_PASSWORDслучайныйпароль первого владельцаSECRET_KEYслучайныйсекрет Flask-сессийCLIENT_DNS1.1.1.1, 8.8.8.8DNS для клиентских конфигурацийNODE_AGENT_TOKENслучайныйсекрет agent APINODE_CODEпустокороткий код ноды: ru, nl, fiNODE_NAMEпустоотображаемое имя нодыNODE_COUNTRYпустокод страныNODE_PUBLIC_URLиз PUBLIC_*URL ноды для главной панели

## Изменение параметров

```bash
cd /opt/xconnect-awg-panel
nano data/panel.env
./install.sh
```

## После смены IP

Измените PUBLIC_HOST, перезапустите установку и обновите base_url на главной панели, если это удалённая нода.

Endpoint записан в выданную конфигурацию. После смены IP клиентам нужен новый конфиг, если вместо IP не использовался постоянный домен.
