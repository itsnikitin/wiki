---
id: OnPlayerLeaveCheckpoint
заголовок: OnPlayerLeaveCheckpoint
описание: Этот callback вызывается, когда игрок покидает контрольную точку, установленную для него в SetPlayerCheckpoint.
тэги: ["player", "checkpoint"]
---

## Описание

Этот callback вызывается, когда игрок покидает контрольную точку, установленную для него в SetPlayerCheckpoint. Одновременно можно установить только одну контрольную точку.

| Имя      | Описание                                             |
| -------- | ---------------------------------------------------- |
| playerid | Идентификатор игрока, покинувшего контрольную точку. |

## Возвращает

Всегда вызывается первым в filterscripts.

## Примеры

```c
public OnPlayerLeaveCheckpoint(playerid)
{
    printf("Игрок %i покинул чекпоинт!", playerid);
    return 1;
}
```

## Примечание

import T from '../../../src/components/templates.js'

<T.TipNPCCallbacks />

## Связанные функции

- [SetPlayerCheckpoint](../functions/SetPlayerCheckpoint.md): Создать контрольную точку для игрока.
- [DisablePlayerCheckpoint](../functions/DisablePlayerCheckpoint.md): Убрать контрольную точку для игрока.
- [IsPlayerInCheckpoint](../functions/IsPlayerInRaceCheckpoint.md): Проверить, находится ли игрок на контрольной точке.
- [SetPlayerRaceCheckpoint](../functions/SetPlayerRaceCheckpoint.md): Создайть контрольную точку гонки для игрока.
- [DisablePlayerRaceCheckpoint](../functions/DisablePlayerRaceCheckpoint.md): Убрать контрольную точку гонки для игрока.
- [IsPlayerInRaceCheckpoint](../functions/IsPlayerInRaceCheckpoint.md): Проверить, находится ли игрок на контрольной точке гонки.
