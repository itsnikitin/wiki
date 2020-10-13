---
id: OnPlayerExitVehicle
заголовок: OnPlayerExitVehicle
описание: Этот callback вызывается, когда игрок начинает выходить из машины.
тэги: ["player", "vehicle"]
---

## Описание

Этот callback вызывается, когда игрок начинает выходить из машины.

| Имя       | Описание                                        | 
| --------- | ----------------------------------------------- |
| playerid  | Идентификатор игрока, выходящего из машины.     |
| vehicleid | Идентификатор машины, из которой игрок выходит. |

## Возвращает

Он всегда вызывается первым в filterscripts.

## Примеры

```c
public OnPlayerExitVehicle(playerid, vehicleid)
{
    new string[35];
    format(string, sizeof(string), "Информация: Вы выходите из машины %i", vehicleid);
    SendClientMessage(playerid, 0xFFFFFFFF, string);
    return 1;
}
```

## Примечание

:::warning

Не вызывается, если игрок падает с велосипеда или его выкидывают с автомобиля другими способами, например с помощью SetPlayerPos. Вы должны использовать OnPlayerStateChange и проверить, является ли старое состояние игрока `PLAYER_STATE_DRIVER` или `PLAYER_STATE_PASSENGER`, а новым состоянием `PLAYER_STATE_ONFOOT`.

:::

## Связанные функции

- [RemovePlayerFromVehicle](../functions/RemovePlayerFromVehicle.md): Выкинуть игрока из машины.
- [GetPlayerVehicleSeat](../functions/GetPlayerVehicleSeat.md): Проверьте, на каком месте находится игрок.
