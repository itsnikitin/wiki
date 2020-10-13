---
id: OnPlayerDisconnect
заголовок: OnPlayerDisconnect
описание: Этот callback вызывается, когда игрок отключается от сервера.
tags: ["player"]
---

## Описание

Этот callback вызывается, когда игрок отключается от сервера.

| Имя      | Описание                                           |
| -------- | -------------------------------------------------- |
| playerid | Идентификатор игрока, который отключился.          |
| reason   | Причина отключения. Смотрите таблицу ниже.         |

## Возвращает

1 - Не позволяет другим filterscripts использовать этот callback.

0 - Указывает, что этот callback будет передан в следующий filterscript.

В filterscripts он всегда вызывается первым

## Примеры

```c
public OnPlayerDisconnect(playerid, reason)
{
    new
        szString[64],
        playerName[MAX_PLAYER_NAME];

    GetPlayerName(playerid, playerName, MAX_PLAYER_NAME);

    new szDisconnectReason[3][] =
    {
        "Тайм-аут/Crash",
        "Выход",
        "Kick/Ban"
    };

    format(szString, sizeof szString, "%s вышел с сервера (%s).", playerName, szDisconnectReason[reason]);

    SendClientMessageToAll(0xC4C4C4FF, szString);
    return 1;
}
```

## Примечание

:::tip

Некоторые функции могут работать некорректно при использовании в этом callback, потому что игрок уже отключен, когда вызывается callback. Это означает, что вы не можете получить однозначную информацию из таких функций, как GetPlayerIp и GetPlayerPos.

:::

## Связанные функции
