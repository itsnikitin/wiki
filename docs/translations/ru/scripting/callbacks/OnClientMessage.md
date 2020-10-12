---
id: OnClientMessage
заголовок: OnClientMessage
описание: Этот callback вызывается всякий раз, когда NPC видит ClientMessage.
тэги: []
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='NPC callback' version='SA-MP 0.3a' />

## Description

Этот callback вызывается всякий раз, когда NPC видит ClientMessage. Этот callback будет срабатывать каждый раз, когда используется функция SendClientMessageToAll, и каждый раз, когда функция SendClientMessage отправляется к NPC. Этот callback не будет вызываться, когда кто-то что-то скажет. Для этого смотрите NPC:OnPlayerText.

| Имя    | Описание                        |
| ------ | ------------------------------- |
| color  | Цвет сообщения ClientMessage.   |
| text[] | Текст сообщения.                |

## Возвращает

Этот callback ничего не возвращает.

## Примеры

```c
public OnClientMessage(color, text[])
{
    if (strfind(text,"Баланс банка: $0") != -1)
    {
        SendClientMessage(playerid, -1, "Я беден :(");
    }
}
```

## Связанные функции
