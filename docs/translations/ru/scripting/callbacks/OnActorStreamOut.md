---
id: OnActorStreamOut
заголовок: OnActorStreamOut
описание: Этот callback вызывается, когда актер исчезает из стрима клиента игрока.
тэги: []
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3.7' />

## Description

Этот callback вызывается, когда актер исчезает из стрима клиента игрока.

| Имя         | Описание                                                       |
| ----------- | -------------------------------------------------------------- |
| actorid     | Идентификатор актера, который исчезает в зоне стрима игрока..  |
| forplayerid | Идентификатор игрока, для которого исчезает актер.             |

## Возвращает

Этот callback всегда вызывается первым из filterscripts.

## Примеры

```c
public OnActorStreamOut(actorid, forplayerid)
{
    new string[40];
    format(string, sizeof(string), "Актер %d больше не в зоне Вашего стрима.", actorid);
    SendClientMessage(forplayerid, 0xFFFFFFFF, string);
    return 1;
}
```

## Примечание

:::tip

Этот callback также может быть вызван NPC.

:::

## Связанные функции
