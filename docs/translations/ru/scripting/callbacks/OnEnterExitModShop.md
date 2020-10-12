---
id: OnEnterExitModShop
заголовок: OnEnterExitModShop
описание: Этот callback вызывается, когда игрок входит или выходит из магазина тюнинга автомобиля.
тэги: []
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3a' />

## Description

Этот callback вызывается, когда игрок входит или выходит из магазина тюнинга автомобиля.

| Имя        | Описание                                                                     |
| ---------- | ---------------------------------------------------------------------------- |
| playerid   | Идентификатор игрока, который вошел в магазин или вышел из него.             |
| enterexit  | 1, если игрок вошел, или 0, если он вышел                                    |
| interiorid | Идентификатор интерьера магазина, в который входит игрок (или 0 при выходе)  |

## Возвращает

Этот callback всегда вызывается первым из filterscripts.

## Примеры

```c
public OnEnterExitModShop(playerid, enterexit, interiorid)
{
    if (enterexit == 0) // Если enterexit равен 0, это означает, что он выходит.
    {
        SendClientMessage(playerid, COLOR_WHITE, "Крутая машина! Вы заплатили налог 100 долларов.");
        GivePlayerMoney(playerid, -100);
    }
    return 1;
}
```

## Заметки

:::warning

Известная ошибка(-и): игроки сталкиваются, когда попадают в один и тот же магазин.

:::

## Связанные функции

- [AddVehicleComponent](../functions/AddVehicleComponent.md): Добавить компонент в автомобиль.
