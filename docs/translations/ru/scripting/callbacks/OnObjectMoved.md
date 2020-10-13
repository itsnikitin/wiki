---
id: OnObjectMoved
заголовок: OnObjectMoved
описание: Этот callback вызывается, когда объект двигается после функции MoveObject (когда он перестает двигаться).
тэги: []
---

## Описание

Этот callback вызывается, когда объект двигается после функции MoveObject (когда он перестает двигаться).

| Имя      | Описание                                       |
| -------- | ---------------------------------------------- |
| objectid | Идентификатор объекта, который был перемещен   |

## Возвращает

В filterscripts он всегда вызывается первым.

## Примеры

```c
public OnObjectMoved(objectid)
{
    printf("Объект %d закончил движение.", objectid);
    return 1;
}
```

## Заметки

:::tip

SetObjectPos не работает при использовании в этом callback. Чтобы исправить это, создайте объект заного.

:::

## Related Functions

- [MoveObject](../functions/MoveObject.md): Переместить объект.
- [MovePlayerObject](../functions/MovePlayerObject.md): Переместить объект игрока.
- [IsObjectMoving](../functions/IsObjectMoving.md): Проверить, движется ли объект.
- [StopObject](../functions/StopObject.md): Остановить движение объекта.
- [OnPlayerObjectMoved](OnPlayerObjectMoved.md): Вызывается, когда объект игрока перестает двигаться.
