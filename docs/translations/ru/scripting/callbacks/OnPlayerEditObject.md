---
id: OnPlayerEditObject
заголовок: OnPlayerEditObject
описание: Этот callback вызывается, когда игрок заканчивает редактирование объекта (EditObject / EditPlayerObject).
тэги: ["player"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3e' />

## Описание

Этот callback вызывается, когда игрок заканчивает редактирование объекта (EditObject / EditPlayerObject).

| Имя          | Описание                                                           |
| ------------ | ------------------------------------------------------------------ |
| playerid     | Идентификатор игрока, который редактировал объект                  |
| playerobject | 0, если это глобальный объект, или 1, если это объект игрока       |
| objectid     | Идентификатор редактируемого объекта                               |
| response     | [Тип ответа](../resources/objecteditionresponsetypes.md)           |
| Float:fX     | Смещение по X для редактируемого объекта                           |
| Float:fY     | Смещение по Y для редактируемого объекта                           |
| Float:fZ     | Смещение по Z для редактируемого объекта                           |
| Float:fRotX  | Поворот по оси X редактируемого объекта                            |
| Float:fRotY  | Поворот по оси Y редактируемого объекта                            |
| Float:fRotZ  | Поворот по оси Z редактируемого объекта                            |

## Возвращает

1 - Не позволяет другим filterscripts использовать этот callback.

0 - Указывает, что этот callback будет передан в следующий filterscript.

В filterscripts он всегда вызывается первым

## Примеры

```c
public OnPlayerEditObject(playerid, playerobject, objectid, response, Float:fX, Float:fY, Float:fZ, Float:fRotX, Float:fRotY, Float:fRotZ)
{
    new
        Float: oldX,
        Float: oldY,
        Float: oldZ,
        Float: oldRotX,
        Float: oldRotY,
        Float: oldRotZ;

    GetObjectPos(objectid, oldX, oldY, oldZ);
    GetObjectRot(objectid, oldRotX, oldRotY, oldRotZ);
    if (!playerobject) // Если это глобальный объект, синхронизируйте позицию для других игроков
    {
        if (!IsValidObject(objectid))
        {
            return 1;
        }
        SetObjectPos(objectid, fX, fY, fZ);
        SetObjectRot(objectid, fRotX, fRotY, fRotZ);
    }

    switch (response)
    {
        case EDIT_RESPONSE_FINAL:
        {
            // Игрок нажал на иконку сохранения
            // Сделайте что-нибудь здесь, чтобы сохранить обновленное положение (и поворот) объекта.
        }

        case EDIT_RESPONSE_CANCEL:
        {
            // Игрок отменил редактирование, поэтому верните объект на прежнее место.
            if (!playerobject) // Объект не является объектом игрока
            {
                SetObjectPos(objectid, oldX, oldY, oldZ);
                SetObjectRot(objectid, oldRotX, oldRotY, oldRotZ);
            }
            else
            {
                SetPlayerObjectPos(playerid, objectid, oldX, oldY, oldZ);
                SetPlayerObjectRot(playerid, objectid, oldRotX, oldRotY, oldRotZ);
            }
        }
    }
    return 1;
}
```

## Примечание

:::warning

При использовании 'EDIT_RESPONSE_UPDATE' имейте в виду, что этот callback не будет вызываться при текущем редактировании, в результате чего последнее обновление 'EDIT_RESPONSE_UPDATE' не будет синхронизировано с текущей позицией объектов.

:::

## Связанные функции

- [EditObject](../functions/EditObject.md): Редактирование объекта.
- [CreateObject](../functions/CreateObject.md): Создание объекта.
- [DestroyObject](../functions/DestroyObject.md): Удаление объекта.
- [MoveObject](../functions/MoveObject.md): Перемещение объекта.
