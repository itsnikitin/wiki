---
id: OnPlayerInteriorChange
заголовок: OnPlayerInteriorChange
описание: Вызывается, когда игрок меняет интерьер.
тэги: ["player"]
---

## Описание

Вызывается, когда игрок меняет интерьер. Может быть вызван при использовании SetPlayerInterior или когда игрок входит/выходит из здания.

| Имя           | Описание                                      |
| ------------- | --------------------------------------------- |
| playerid      | Игрок, изменивший интерьер.                   |
| newinteriorid | Интерьер, в котором сейчас находится игрок.   |
| oldinteriorid | Интерьер, в котором был игрок раньше.         |

## Возвращает

Всегда вызывается первым в игровом режиме.

## Примеры

```c
public OnPlayerInteriorChange(playerid, newinteriorid, oldinteriorid)
{
    new string[42];
    format(string, sizeof(string), "Вы перешли из интерьера %d в интерьер %d!", oldinteriorid, newinteriorid);
    SendClientMessage(playerid, COLOR_ORANGE, string);
    return 1;
}
```

## Связанные функции

- [SetPlayerInterior](../functions/SetPlayerInterior.md): Изменить интерьер игрока.
- [GetPlayerInterior](../functions/GetPlayerInterior.md): Получить текущий интерьер игрока.
- [LinkVehicleToInterior](../functions/LinkVehicleToInterior.md): Изменить интерьер, в котором будет виден автомобиль.
- [OnPlayerStateChange](OnPlayerStateChange.md): Вызывается, когда игрок меняет состояние.
