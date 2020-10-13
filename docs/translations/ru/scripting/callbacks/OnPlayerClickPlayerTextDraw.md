---
id: OnPlayerClickPlayerTextDraw
заголовок: OnPlayerClickPlayerTextDraw
описание: Этот callback вызывается, когда игрок нажимает на PlayerTextDraw.
tags: ["player", "textdraw", "playertextdraw"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3e' />

## Описание

Этот callback вызывается, когда игрок нажимает на PlayerTextDraw. Он не вызывается, когда игрок отменяет режим выбора (ESC) - однако `OnPlayerClickTextDraw` вызывается.

| Имя          | Описание                                                |
| ------------ | ------------------------------------------------------- |
| playerid     | Идентификатор игрока, кликнувшего PlayerTextDraw.       |
| playertextid | Идентификатор текстдрава, который нажал игрок.          |

## Возвращает

Он всегда вызывается первым в filterscripts, поэтому возврат `1` также блокирует его просмотр для filterscripts.

## Примеры

```c
new PlayerText:gPlayerTextDraw[MAX_PLAYERS];

public OnPlayerConnect(playerid)
{
    // Создание текстдрава
    gPlayerTextDraw[playerid] = CreatePlayerTextDraw(playerid, 10.000000, 141.000000, "MyTextDraw");
    PlayerTextDrawTextSize(playerid, gPlayerTextDraw[playerid], 60.000000, 20.000000);
    PlayerTextDrawAlignment(playerid, gPlayerTextDraw[playerid],0);
    PlayerTextDrawBackgroundColor(playerid, gPlayerTextDraw[playerid],0x000000ff);
    PlayerTextDrawFont(playerid, gPlayerTextDraw[playerid], 1);
    PlayerTextDrawLetterSize(playerid, gPlayerTextDraw[playerid], 0.250000, 1.000000);
    PlayerTextDrawColor(playerid, gPlayerTextDraw[playerid], 0xffffffff);
    PlayerTextDrawSetProportional(playerid, gPlayerTextDraw[playerid], 1);
    PlayerTextDrawSetShadow(playerid, gPlayerTextDraw[playerid], 1);

    // Делаем его кликабельным
    PlayerTextDrawSetSelectable(playerid, gPlayerTextDraw[playerid], 1);

    // Показываем его игроку
    PlayerTextDrawShow(playerid, gPlayerTextDraw[playerid]);
    return 1;
}

public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
    if (newkeys == KEY_SUBMISSION)
    {
        SelectTextDraw(playerid, 0xFF4040AA);
    }
    return 1;
}

public OnPlayerClickPlayerTextDraw(playerid, PlayerText:playertextid)
{
    if (playertextid == gPlayerTextDraw[playerid])
    {
         SendClientMessage(playerid, 0xFFFFFFAA, "Вы кликнули по текстдраву");
         CancelSelectTextDraw(playerid);
         return 1;
    }
    return 0;
}
```

## Примечание

:::warning

Когда игрок нажимает ESC, чтобы отменить выбор текстдрава, вызывается OnPlayerClickTextDraw с идентификатором отрисовки «INVALID_TEXT_DRAW». OnPlayerClickPlayerTextDraw также вызываться не будет.

:::

## Связанные функции

- [PlayerTextDrawSetSelectable](../functions/PlayerTextDrawSetSelectable.md): Устанавливает, можно ли выбрать текстдрав игрока через SelectTextDraw.
- [OnPlayerClickTextDraw](OnPlayerClickTextDraw.md): Вызывается когда игрок кликает по текстдраву.
- [OnPlayerClickPlayer](OnPlayerClickPlayer.md): Вызывается, когла игрок кликает по другому игроку.
