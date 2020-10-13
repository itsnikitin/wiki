---
id: OnPlayerEnterRaceCheckpoint
заголовок: OnPlayerEnterRaceCheckpoint
описание: Этот callback вызывается, когда игрок входит в контрольную точку гонки.
тэги: ["player", "checkpoint", "racecheckpoint"]
---

## Описание

Этот callback вызывается, когда игрок входит в контрольную точку гонки.

| Имя      | Описание                                              |
| -------- | ----------------------------------------------------- |
| playerid | The ID of the player who entered the race checkpoint. |

## Возвращает

В filterscripts он всегда вызывается первым.

## Примеры

```c
public OnPlayerEnterRaceCheckpoint(playerid)
{
    printf("Игрок %d вошел в контрольную точку гонки!", playerid);
    return 1;
}
```

## Примечание

import T from '../../../src/components/templates.js'

<T.TipNPCCallbacks />

## Связанные функции

- [SetPlayerCheckpoint](../functions/SetPlayerCheckpoint.md): Создание контрольной точки для игрока.
- [DisablePlayerCheckpoint](../functions/DisablePlayerCheckpoint.md): Отключить текущую контрольную точку игрока.
- [IsPlayerInCheckpoint](../functions/IsPlayerInRaceCheckpoint.md): Проверить, находится ли игрок на контрольной точке.
- [SetPlayerRaceCheckpoint](../functions/SetPlayerRaceCheckpoint.md): Создание контрольную точку гонки для игрока.
- [DisablePlayerRaceCheckpoint](../functions/DisablePlayerRaceCheckpoint.md): Отключить контрольную точку гонки для игрока.
- [IsPlayerInRaceCheckpoint](../functions/IsPlayerInRaceCheckpoint.md): Проверить, находится ли игрок на контрольной точке гонки.
