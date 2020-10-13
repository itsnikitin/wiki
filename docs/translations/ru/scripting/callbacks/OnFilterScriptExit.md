---
id: OnFilterScriptExit
заголовок: OnFilterScriptExit
описание: Этот callback вызывается при выгрузке filtercsript.
тэги: []
---

## Описание

Этот callback вызывается при выгрузке filtercsript. Он вызывается только внутри выгружаемого filtercsript.

## Примеры

```c
public OnFilterScriptExit()
{
    print("\n--------------------------------------");
    print("Мой filterscript выгружен.");
    print("--------------------------------------\n");
    return 1;
}
```

## Связанные функции
