---
id: OnPlayerClickTextDraw
заголовок: OnPlayerClickTextDraw
описание: Этот callback вызывается, когда игрок нажимает на текстдрав или отменяет режим выбора с помощью клавиши Escape.
тэги: ["player", "textdraw"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3e' />

## Описание

Этот callback вызывается, когда игрок нажимает на текстдрав или отменяет режим выбора с помощью клавиши Escape.

| Имя       | Описание                                                                        |
| --------- | ------------------------------------------------------------------------------- |
| playerid  | Идентификатор игрока, который кликнул текстдрав                                 |
| clickedid | Идентификатор кликнутого текстдрава. INVALID_TEXT_DRAW, если выбор был отменен. |

## Возвращает

Он всегда вызывается первым в filterscripts, поэтому возвращение 1 также блокирует его просмотр другими скриптами.

## Примеры

```c
new Text:gTextDraw;

public OnGameModeInit()
{
    gTextDraw = TextDrawCreate(10.000000, 141.000000, "MyTextDraw");
    TextDrawTextSize(gTextDraw,60.000000, 20.000000);
    TextDrawAlignment(gTextDraw,0);
    TextDrawBackgroundColor(gTextDraw,0x000000ff);
    TextDrawFont(gTextDraw,1);
    TextDrawLetterSize(gTextDraw,0.250000, 1.000000);
    TextDrawColor(gTextDraw,0xffffffff);
    TextDrawSetProportional(gTextDraw,1);
    TextDrawSetShadow(gTextDraw,1);
    TextDrawSetSelectable(gTextDraw, 1);
    return 1;
}

public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
    if (newkeys == KEY_SUBMISSION)
    {
        TextDrawShowForPlayer(playerid, gTextDraw);
        SelectTextDraw(playerid, 0xFF4040AA);
    }
    return 1;
}

public OnPlayerClickTextDraw(playerid, Text:clickedid)
{
    if (clickedid == gTextDraw)
    {
         SendClientMessage(playerid, 0xFFFFFFAA, "Вы кликнули на текстдрав.");
         CancelSelectTextDraw(playerid);
         return 1;
    }
    return 0;
}
```

## Примечание

:::warning

Интерактивная область текстдрава определяется функцией TextDrawTextSize. Параметры x и y, передаваемые этой функции, не должны быть нулевыми или отрицательными. Не используйте CancelSelectTextDraw в этом callback. Это приводит к бесконечному циклу.

:::

## Связанные функции

- [OnPlayerClickPlayerTextDraw](OnPlayerClickPlayerTextDraw.md): Вызывается, когда игрок нажимает на PlayerTextDraw.
- [OnPlayerClickPlayer](OnPlayerClickPlayer.md): Вызывается, когда игрок выбирает другого игрока.
