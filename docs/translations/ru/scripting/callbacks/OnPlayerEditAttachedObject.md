---
id: OnPlayerEditAttachedObject
заголовок: OnPlayerEditAttachedObject
описание: Этот callback вызывается, когда игрок завершает режим редактирования прикрепленного объекта.
тэги: ["player"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3e' />

## Описание

Этот callback вызывается, когда игрок завершает режим редактирования прикрепленного объекта.

| Имя            | Описание                                                                   |
| -------------- | -------------------------------------------------------------------------- |
| playerid       | Идентификатор игрока, вышедшего из режима редактирования                   |
| response       | 0, если отменили (ESC), или 1, если щелкнули значок сохранения             |
| modelid        | Модель прикрепленного объекта, который редактировался                      |
| boneid         | Кость, на которой редактировался прикрепленный объект                      |
| Float:fOffsetX | Смещение X прикрепленного объекта, который был отредактирован              |
| Float:fOffsetY | Смещение Y прикрепленного объекта, который был отредактирован              |
| Float:fOffsetZ | Смещение Z прикрепленного объекта, который был отредактирован              |
| Float:fRotX    | Поворот по оси X для прикрепленного объекта, который был отредактирован    |
| Float:fRotY    | Поворот по оси Y для прикрепленного объекта, который был отредактирован    |
| Float:fRotZ    | Поворот по оси Z для прикрепленного объекта, который был отредактирован    |
| Float:fScaleX  | Масштаб X прикрепленного объекта, который редактировался                   |
| Float:fScaleY  | Масштаб Y прикрепленного объекта, который редактировался                   |
| Float:fScaleZ  | Масштаб Z прикрепленного объекта, который редактировался                   |

## Возвращает

1 - Не позволяет другим filterscripts использовать этот callback.

0 - Указывает, что этот callback будет передан в следующий filterscript.

В filterscripts он всегда вызывается первым

## Примеры

```c
enum attached_object_data
{
    Float:ao_x,
    Float:ao_y,
    Float:ao_z,
    Float:ao_rx,
    Float:ao_ry,
    Float:ao_rz,
    Float:ao_sx,
    Float:ao_sy,
    Float:ao_sz
}

new ao[MAX_PLAYERS][MAX_PLAYER_ATTACHED_OBJECTS][attached_object_data];

// При присоединении прикрепленных объектов данные должны храниться в указанном выше массиве.

public OnPlayerEditAttachedObject(playerid, response, index, modelid, boneid, Float:fOffsetX, Float:fOffsetY, Float:fOffsetZ, Float:fRotX, Float:fRotY, Float:fRotZ, Float:fScaleX, Float:fScaleY, Float:fScaleZ)
{
    if (response)
    {
        SendClientMessage(playerid, COLOR_GREEN, "Изменения прикрепленного объекта сохранены.");

        ao[playerid][index][ao_x] = fOffsetX;
        ao[playerid][index][ao_y] = fOffsetY;
        ao[playerid][index][ao_z] = fOffsetZ;
        ao[playerid][index][ao_rx] = fRotX;
        ao[playerid][index][ao_ry] = fRotY;
        ao[playerid][index][ao_rz] = fRotZ;
        ao[playerid][index][ao_sx] = fScaleX;
        ao[playerid][index][ao_sy] = fScaleY;
        ao[playerid][index][ao_sz] = fScaleZ;
    }
    else
    {
        SendClientMessage(playerid, COLOR_RED, "Изменения прикрепленного объекта не сохраняются.");

        new i = index;
        SetPlayerAttachedObject(playerid, index, modelid, boneid, ao[playerid][i][ao_x], ao[playerid][i][ao_y], ao[playerid][i][ao_z], ao[playerid][i][ao_rx], ao[playerid][i][ao_ry], ao[playerid][i][ao_rz], ao[playerid][i][ao_sx], ao[playerid][i][ao_sy], ao[playerid][i][ao_sz]);
    }
    return 1;
}
```

## Примечание

:::warning

Изменения следует отклонить, если ответ '0' (отменен). Это необходимо сделать, сохранив смещения и т.д. в массиве ДО использования EditAttachedObject.

:::

## Связанные функции

- [EditAttachedObject](../functions/EditAttachedObject.md): Редактировать прикрепленный объект.
- [SetPlayerAttachedObject](../functions/SetPlayerAttachedObject.md): Крепит объект к игроку.
