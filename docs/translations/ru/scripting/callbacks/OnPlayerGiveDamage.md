---
id: OnPlayerGiveDamage
заголовок: OnPlayerGiveDamage
описание: Этот callback вызывается, когда игрок наносит урон другому игроку.
тэги: ["player"]
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3d' />

## Описание

Этот callback вызывается, когда игрок наносит урон другому игроку.

| Имя       | Описание                                                                                                                                 |
| --------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| playerid  | Идентификатор игрока, нанесшего урон.                                                                                                    |
| damagedid | Идентификатор игрока, получившего урон.                                                                                                  |
| amount    | Количество потерянных здоровья/брони (вместе).                                                                                           |
| weaponid  | Причина, по которой был нанесен урон.                                                                                                    |
| bodypart  | Часть тела, в которую попали. (ПРИМЕЧАНИЕ: этот параметр был добавлен в 0.3z. Не используйте его, если используете более старую версию!) |

## Возвращает

1 - Сallback не будет вызываться в других filterscripts.

0 - Позволяет вызывать этот callback в других filterscripts.

Он всегда вызывается первым в filterscripts, поэтому возвращение `1` блокирует его просмотр другими скриптами.

## Примеры

```c
public OnPlayerGiveDamage(playerid, damagedid, Float:amount, weaponid, bodypart)
{
    new string[128], victim[MAX_PLAYER_NAME], attacker[MAX_PLAYER_NAME];
    new weaponname[24];
    GetPlayerName(playerid, attacker, sizeof (attacker));
    GetPlayerName(damagedid, victim, sizeof (victim));

    GetWeaponName(weaponid, weaponname, sizeof (weaponname));
    format(string, sizeof(string), "%s нанес %.0f урона %s, оружие:%s, часть тела:%d", attacker, amount, victim, weaponname, bodypart);
    SendClientMessageToAll(0xFFFFFFFF, string);
    return 1;
}
```

## Примечание

:::tip

Имейте в виду, что в некоторых случаях эта функция может быть неточной. Если вы хотите, чтобы некоторые игроки не наносили вред друг другу, используйте SetPlayerTeam. Weaponid вернет 37 (огнемет) из любых источников огня (например, молотов, 18). Weaponid вернет 51 из любого оружия, которое создает взрыв (например, РПГ, граната). Playerid - единственный, кто может вызвать callback. Amount - это всегда максимальный урон, который может нанести weaponid, даже если оставшееся здоровье меньше этого максимального урона. Таким образом, когда у игрока 100,0 здоровья и он получает выстрел из Desert Eagle с повреждением 46,2, ему нужно 3 выстрела, чтобы убить этого игрока. Все 3 выстрела покажут количество 46,2, даже если после последнего выстрела у игрока останется только 7,6 здоровья.

:::

## Связанные функции
