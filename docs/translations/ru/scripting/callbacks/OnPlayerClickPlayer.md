---
id: OnPlayerClickPlayer
заголовок: OnPlayerClickPlayer
описание: Вызывается, когда игрок дважды щелкает по игроку в таблице игроков (Tab).
тэги: ["player"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3a' />

## Описание

Вызывается, когда игрок дважды щелкает по игроку в таблице игроков (Tab).

| Имя             | Описание                                                         |
| --------------- | ---------------------------------------------------------------- |
| playerid        | Идентификатор игрока, который щелкнул по игроку                  |
| clickedplayerid | Идентификатор игрока, по которому был выполнен клик.             |
| source          | Источник клика игрока.                                           |

## Возвращает

1 - Не позволяет другим filterscripts использовать этот callback.

0 - Указывает, что этот callback будет передан в следующий filterscript.

В filterscripts он всегда вызывается первым.

## Примеры

```c
public OnPlayerClickPlayer(playerid, clickedplayerid, source)
{
    new message[32];
    format(message, sizeof(message), "Вы кликнули по игроку %d", clickedplayerid);
    SendClientMessage(playerid, 0xFFFFFFFF, message);
    return 1;
}
```

## Примечание

:::tip

В настоящее время существует только один «источник» (0 - CLICK_SOURCE_SCOREBOARD). Существование этого аргумента предполагает, что в будущем может поддерживаться больше источников.

:::

## Связанные функции

- [OnPlayerClickTextDraw](OnPlayerClickTextDraw.md): Вызывается, когда игрок нажимает на TextDraw.
