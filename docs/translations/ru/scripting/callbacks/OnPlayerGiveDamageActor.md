---
id: OnPlayerGiveDamageActor
заголовок: OnPlayerGiveDamageActor
описание: Этот callback вызывается, когда игрок наносит урон актеру.
тэги: ["player"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3.7' />

## Описание

Этот callback вызывается, когда игрок наносит урон актеру.

| Имя             | Описание                                              |
| --------------- | ----------------------------------------------------- |
| playerid        | Идентификатор игрока, нанесшего урон.                 |
| damaged_actorid | Идентификатор актера, получившего повреждения.        |
| amount          | Количество потерянных актером единиц здоровья/брони.  |
| weaponid        | Причина, по которой был нанесен ущерб.                |
| bodypart        | Часть тела, которая была поражена.                    |

## Возвращает

1 - Callback не будет вызываться в других filterscripts.

0 - Позволяет вызывать этот callback в других filterscripts.

Он всегда вызывается первым в filterscripts, поэтому возвращение `1` блокирует его просмотр другими скриптами.

## Примеры

```c
public OnPlayerGiveDamageActor(playerid, damaged_actorid, Float: amount, weaponid, bodypart)
{
    new string[128], attacker[MAX_PLAYER_NAME];
    new weaponname[24];
    GetPlayerName(playerid, attacker, sizeof (attacker));
    GetWeaponName(weaponid, weaponname, sizeof (weaponname));

    format(string, sizeof(string), "%s нанес %.0f урон актеру с идентификатором %d, оружие: %s", attacker, amount, damaged_actorid, weaponname);
    SendClientMessageToAll(0xFFFFFFFF, string);
    return 1;
}
```

## Примечание

:::tip

Эта функция не вызывается, если актер установлен неуязвимым (ПО УМОЛЧАНИЮ). Смотрите [SetActorInvulnerable](../functions/SetActorInvulnerable.md).

:::

## Связанные функции

- [CreateActor](../functions/CreateActor.md): Создать актера (статический NPC).
- [SetActorInvulnerable](../functions/SetActorInvulnerable.md): Сделать актера неуязвимым.
- [SetActorHealth](../functions/SetActorHealth.md): Установить здоровье актера.
- [GetActorHealth](../functions/GetActorHealth.md): Получить здоровье актера.
- [IsActorInvulnerable](../functions/IsActorInvulnerable.md): Проверить уязвимость актера.
- [IsValidActor](../functions/IsValidActor.md): Проверить, действителен ли идентификатор актера.
- [OnActorStreamOut](OnActorStreamOut.md): Вызывается, когда актер появляется в стриме игрока.
- [OnPlayerStreamIn](OnPlayerStreamIn.md): Вызывается, когда игрок появляется для другого игрока.
