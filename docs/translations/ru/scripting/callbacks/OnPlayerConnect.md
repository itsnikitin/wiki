---
id: OnPlayerConnect
заголовок: OnPlayerConnect
описание: Этот callback вызывается, когда игрок подключается к серверу.
тэги: ["player"]
---

## Описание

Этот callback вызывается, когда игрок подключается к серверу.

| Имя      | Описание                             |
| -------- | ------------------------------------ |
| playerid | Идентификатор подключенного игрока.  |

## Возвращает

1 - Не позволяет другим filterscripts использовать этот callback.

0 - Указывает, что этот callback будет передан в следующий filterscript.

В filterscripts он всегда вызывается первым.

## Примеры

```c
public OnPlayerConnect(playerid)
{
    new
        string[64],
        playerName[MAX_PLAYER_NAME];

    GetPlayerName(playerid, playerName, MAX_PLAYER_NAME);
    format(string, sizeof string, "%s подключился к серверу. Добро пожаловать!", playerName);
    SendClientMessageToAll(0xFFFFFFAA, string);
    return 1;
}
```

## Примечание

import T from '../../../src/components/templates.js'

<T.TipNPCCallbacks />

## Связанные функции
