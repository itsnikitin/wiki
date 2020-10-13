---
id: OnPlayerEnterCheckpoint
заголовок: OnPlayerEnterCheckpoint
описание: Этот callback вызывается, когда игрок входит в контрольную точку, установленную для этого игрока.
тэги: ["player", "checkpoint"]
---

## Описание

Этот callback вызывается, когда игрок входит в контрольную точку, установленную для этого игрока.

| Имя      | Описание                               |
| -------- | -------------------------------------- |
| playerid | Игрок, вошедший на контрольную точку.  |

## Возвращает

В filterscripts он всегда вызывается первым.

## Примеры

```c
// В этом примере контрольная точка создается для игрока при появлении,
// который создает автомобиль и отключает контрольную точку.
public OnPlayerSpawn(playerid)
{
    SetPlayerCheckpoint(playerid, 1982.6150, -220.6680, -0.2432, 3.0);
    return 1;
}

public OnPlayerEnterCheckpoint(playerid)
{
    CreateVehicle(520, 1982.6150, -221.0145, -0.2432, 82.2873, -1, -1, 60000);
    DisablePlayerCheckpoint(playerid);
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
