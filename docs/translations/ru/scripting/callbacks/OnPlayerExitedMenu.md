---
id: OnPlayerExitedMenu
заголовок: OnPlayerExitedMenu
описание: Вызывается, когда игрок выходит из меню.
тэги: ["player", "menu"]
---

## Описание

Вызывается, когда игрок выходит из меню.

| Имя      | Описание                                  |
| -------- | ----------------------------------------- |
| playerid | Идентификатор игрока, вышедшего из меню   |

## Возвращает

Всегда вызывается первым в игровом режиме.

## Примеры

```c
public OnPlayerExitedMenu(playerid)
{
    TogglePlayerControllable(playerid,1); // разморозить игрока при выходе из меню
    return 1;
}
```

## Связанные функции

- [CreateMenu](../functions/CreateMenu.md): Создать меню.
- [DestroyMenu](../functions/DestroyMenu.md): Уничтожить меню.
