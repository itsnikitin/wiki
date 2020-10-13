---
id: OnDialogResponse
заголовок: OnDialogResponse
описание: Этот callback вызывается, когда игрок отвечает на диалоговое окно, отображаемое с помощью ShowPlayerDialog, щелчком кнопки, нажатием ENTER / ESC или двойным щелчком элемента списка (при использовании диалогового окна стиля списка).
тэги: []
---

import T from '../../../src/components/templates.js'

<T.VersionWarn name='callback' version='SA-MP 0.3a' />

## Описание

Этот callback вызывается, когда игрок отвечает на диалоговое окно, отображаемое с помощью ShowPlayerDialog, щелчком кнопки, нажатием ENTER / ESC или двойным щелчком элемента списка (при использовании диалогового окна стиля списка).

| Имя         | Описание                                                                                                                                     |
| ----------- | -------------------------------------------------------------------------------------------------------------------------------------------- |
| playerid    | Идентификатор игрока, ответившего на диалог.                                                                                                 |
| dialogid    | Идентификатор диалога, на который ответил игрок, указанный в ShowPlayerDialog.                                                               |
| response    | 1 для левой кнопки и 0 для правой кнопки (если отображается только одна кнопка — всегда 1)                                                   |
| listitem    | Идентификатор элемента списка, выбранного игроком (начинается с 0) (только при использовании диалогового окна стиля списка, иначе будет -1). |
| inputtext[] | Текст, введенный игроком в поле ввода, или текст выбранного элемента списка.                                                                 |

## Возвращает

Callback всегда вызывается первым в filterscripts, поэтому возвращение 1 блокирует его просмотр другими скриптами.

## Примеры

```c
// Определим идентификатор диалога, чтобы могли обрабатывать ответы
#define DIALOG_RULES 1

// В какой-нибудь команде
ShowPlayerDialog(playerid, DIALOG_RULES, DIALOG_STYLE_MSGBOX, "Правила сервера", "- Не читерить\n- Не спамить\n- Уважать администрацию\n\nВы принимаете эти правила?", "Да", "Нет");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_RULES)
    {
        if (response) // Если нажато 'Да' или нажат Enter
        {
            SendClientMessage(playerid, COLOR_GREEN, "Спасибо, что согласились с правилами сервера!");
        }
        else // Нажат Esc или кнопка 'Нет'
        {
            Kick(playerid);
        }
        return 1; // Мы обработали диалог, поэтому возвращаем 1. Точно так же, как в OnPlayerCommandText.
    }

    return 0; // Вы ДОЛЖНЫ вернуть 0 здесь! Как и в OnPlayerCommandText.
}

#define DIALOG_LOGIN 2

// В какой-нибудь команде
ShowPlayerDialog(playerid, DIALOG_LOGIN, DIALOG_STYLE_INPUT, "Авторизация", "Пожалуйста введите Ваш пароль", "Логин", "Закрыть");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_LOGIN)
    {
        if (!response) // Нажат Esc или кнопка 'Закрыть'
        {
            Kick(playerid);
        }
        else // Если нажато 'Логин' или нажат Enter
        {
            if (CheckPassword(playerid, inputtext))
            {
                SendClientMessage(playerid, COLOR_RED, "Вы вошли в систему!");
            }
            else
            {
                SendClientMessage(playerid, COLOR_RED, "Ошибка авторизации!");

                // Показываем диалог заного
                ShowPlayerDialog(playerid, DIALOG_LOGIN, DIALOG_STYLE_INPUT, "Авторизация", "Пожалуйста введите Ваш пароль", "Логин", "Закрыть");
            }
        }
        return 1; // Мы обработали диалог, поэтому возвращаем 1. Точно так же, как в OnPlayerCommandText.
    }

    return 0; // Вы ДОЛЖНЫ вернуть 0 здесь! Как и в OnPlayerCommandText.
}

#define DIALOG_WEAPONS 3

// В какой-нибудь команде
ShowPlayerDialog(playerid, DIALOG_WEAPONS, DIALOG_STYLE_LIST, "Оружие", "Desert Eagle\nAK-47\nCombat Shotgun", "Выбрать", "Закрыть");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_WEAPONS)
    {
        if (response) // Если нажато 'Выбрать' или дважды нажат элемент списка
        {
            // Выдаем оружие игроку
            switch(listitem)
            {
                case 0: GivePlayerWeapon(playerid, WEAPON_DEAGLE, 14); // Выдаем desert eagle
                case 1: GivePlayerWeapon(playerid, WEAPON_AK47, 120); // Выдаем AK-47
                case 2: GivePlayerWeapon(playerid, WEAPON_SHOTGSPA, 28); // Выдаем Combat Shotgun
            }
        }
        return 1; // Мы обработали диалог, поэтому возвращаем 1. Точно так же, как в OnPlayerCommandText.
    }

    return 0; // Вы ДОЛЖНЫ вернуть 0 здесь! Как и в OnPlayerCommandText.
}

#define DIALOG_WEAPONS 3

// В какой-нибудь команде
ShowPlayerDialog(playerid, DIALOG_WEAPONS, DIALOG_STYLE_LIST, "Оружие",
"Оружие\tПатроны\tЦена\n\
M4\t120\t500\n\
MP5\t90\t350\n\
AK-47\t120\t400",
"Выбрать", "Закрыть");

public OnDialogResponse(playerid, dialogid, response, listitem, inputtext[])
{
    if (dialogid == DIALOG_WEAPONS)
    {
        if (response) // Если нажато 'Выбрать' или дважды нажат элемент списка
        {
            // Выдаем оружие игроку
            switch(listitem)
            {
                case 0: GivePlayerWeapon(playerid, WEAPON_M4, 120); // Выдаем M4
                case 1: GivePlayerWeapon(playerid, WEAPON_MP5, 90); // Выдаем MP5
                case 2: GivePlayerWeapon(playerid, WEAPON_AK47, 120); // Выдаем AK-47
            }
        }
        return 1; // Мы обработали диалог, поэтому возвращаем 1. Точно так же, как в OnPlayerCommandText.
    }

    return 0; // Вы ДОЛЖНЫ вернуть 0 здесь! Как и в OnPlayerCommandText.
}
```

## Примечание

:::tip

Параметры могут содержать разные значения в зависимости от стиля диалога ([щелкните, чтобы увидеть больше примеров](../resources/dialogstyles.md)).

:::

:::tip

Уместно использовать оператор switch между разными диалоговыми окнами, если у вас их много.

:::

:::warning

Диалог игрока не скрывается при перезапуске игрового режима, в результате чего сервер печатает «Предупреждение: PlayerDialogResponse PlayerId: 0 идентификатор диалога не совпадает с идентификатором последнего отправленного диалога», если игрок ответил на этот диалог после перезапуска.

:::

## Связанные функции

- [ShowPlayerDialog](../functions/ShowPlayerDialog.md): Показать диалог игроку
