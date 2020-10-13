---
id: OnIncomingConnection
заголовок: OnIncomingConnection
описание: Этот callback вызывается, когда IP-адрес пытается подключиться к серверу.
тэги: []
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3z R2-2' />

## Описание

Этот callback вызывается, когда IP-адрес пытается подключиться к серверу. Чтобы заблокировать входящие соединения, используйте BlockIpAddress.

| Имя          | Описание                                           |
| ------------ | -------------------------------------------------- |
| playerid     | Идентификатор игрока, пытающегося подключиться     |
| ip_address[] | IP-адрес игрока, пытающегося подключиться          |
| port         | Порт попытки подключения                           |

## Возвращает

1 - Не позволяет другим filterscripts использовать этот callback.

0 - Указывает, что этот callback будет передан в следующий filterscript.

В filterscripts он всегда вызывается первым.

## Примеры

```c
public OnIncomingConnection(playerid, ip_address[], port)
{
    printf("Входящее соединение для игрока ID %i [IP/port: %s:%i]", playerid, ip_address, port);
    return 1;
}
```

## Связанные функции

- [BlockIpAddress](../functions/BlockIpAddress.md): Заблокируйте IP-адрес для подключения к серверу на установленный период времени.
- [UnBlockIpAddress](../functions/UnBlockIpAddress.md): Разблокируйте IP-адрес, который ранее был заблокирован.
