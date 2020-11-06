---
id: OnPlayerKeyStateChange
заголовок: OnPlayerKeyStateChange
описание: Этот callback вызывается, когда состояние любой поддерживаемой клавиши изменяется (нажата/отпущена).
тэги: ["player"]
---

## Описание

Этот callback вызывается, когда состояние любой [поддерживаемой](../resources/keys.md) клавиши изменяется (нажата/отпущена).<br/>Клавиши управления не запускают OnPlayerKeyStateChange (вверх/вниз/влево/вправо).

| Имя      | Описание                                                                                            |
| -------- | --------------------------------------------------------------------------------------------------- |
| playerid | Идентификатор игрока, который нажал или отпустил клавишу.                                           |
| newkeys  | Карта (битовая маска) клавиш, нажатых в данный момент - [смотрите здесь](../resources/keys.md)      |
| oldkeys  | Карта (битовая маска) клавиш, нажатых до текущего момента - [смотрите здесь](../resources/keys.md). |

## Возвращает

- Этот callback не обрабатывает возвраты.
- Он всегда вызывается первым в игровом режиме.

## Примечание

:::info

Этот callback также может быть вызван NPC.

:::

:::tip

Клавиши управления не вызывают OnPlayerKeyStateChange (вверх/вниз/влево/вправо). <br/>Их можно обнаружить только с помощью [GetPlayerKeys](../functions/GetPlayerKeys.md) (в [OnPlayerUpdate](../callbacks/OnPlayerUpdate.md) или таймере).

:::

## Связанные функции

- [GetPlayerKeys](../functions/GetPlayerKeys.md): Проверить, какие клавиши держит игрок.

## Дополнительная информация

### Вступление

Этот callback вызывается всякий раз, когда игрок нажимает или отпускает одну из поддерживаемых клавиш (см. [Ключи](../resources/keys.md)). <br/> Поддерживаемые клавиши - это не настоящие клавиши клавиатуры, а назначенные функциональные клавиши в San Andreas, это означает, что, например, вы не можете определить, когда кто-то нажимает <strong>Space</strong>, но можете определить, когда нажимают клавишу спринта (которая может быть или не быть назначена пробел (по умолчанию)).

### Параметры

Параметры этой функции представляют собой список всех клавиш, удерживаемых в данный момент, и всех клавиш, удерживаемых момент назад. Callback вызывается при изменении состояния клавиши (то есть при нажатии или отпускании клавиши) и передает состояния или все клавиши до и после этого изменения. Эту информацию можно использовать, чтобы точно увидеть, что произошло, но переменные нельзя использовать напрямую, как параметры для других функций. Чтобы уменьшить количество переменных, для представления ключа используется только один BIT, это означает, что одна переменная может содержать несколько ключей одновременно, и простое сравнение значений не всегда работает.

### Как НЕ проверять клавишу

Предположим, вы хотите определить, когда игрок нажимает кнопку FIRE, очевидным кодом будет:

```c
if (newkeys == KEY_FIRE)
```

Этот код может работать в вашем тестировании, но он неверен и вашего тестирования недостаточно. Попробуйте присесть и нажать огонь - ваш код мгновенно перестанет работать. Почему? Поскольку `newkeys` больше не то же самое, что `KEY_FIRE`, теперь это `KEY_FIRE` в сочетании с `KEY_CROUCH`.

### Как проверить клавишу

Итак, если переменная может содержать несколько ключей одновременно, как проверить только один? Ответ - битовая маскировка. Каждая клавиша имеет свой собственный бит в переменной (некоторые клавиши имеют один и тот же бит, но игрок находится на ногах/в машине, поэтому в любом случае их нельзя нажимать одновременно), и вам нужно проверить только этот единственный бит:

```c
if (newkeys & KEY_FIRE)
```

Обратите внимание, что единственный знак <strong>&</strong> является правильным - это побитовое И, а не логическое И, как два амперсанда.

Теперь, если вы протестируете этот код, он будет работать независимо от того, приседаете ли вы или стоите при нажатии клавиши огня. Однако есть еще одна небольшая проблема - он будет срабатывать, пока вы держите клавишу. OnPlayerKeyStateChange вызывается каждый раз при изменении клавиши, и этот код верен всякий раз, когда зажата клавиша огня. Если вы нажмете огонь, код сработает, если эта клавиша удерживается, и вы нажмете приседание - этот код будет срабатывать снова, потому что клавиша (приседание) изменилась, а огонь все еще удерживается.

### Как проверить, не нажата ли клавиша

Здесь на помощь приходит "oldkeys". Чтобы проверить, была ли только что нажата клавиша, вам нужно сначала проверить, установлена ли она в "newkeys" - то есть она удерживается, а затем проверить, что она НЕ находится в "oldkeys" - т.е. только что была удержана. Следующий код делает это:

```c
if ((newkeys & KEY_FIRE) && !(oldkeys & KEY_FIRE))
```

Это будет верно ТОЛЬКО при первом нажатии клавиши FIRE, а не при ее удерживании и изменении другой клавиши.

### Как проверить, отпущена ли клавиша

Точно такой же принцип, что и выше, но в обратном порядке:

```c
if ((oldkeys & KEY_FIRE) && !(newkeys & KEY_FIRE))
```

### Как проверить наличие нескольких клавиш

Если вы хотите проверить, приседают ли игроки и стреляют, то следующий код будет работать:

```c
if ((newkeys & KEY_FIRE) && (newkeys & KEY_CROUCH))
```

Однако, если вы хотите определить, когда они СНАЧАЛА нажимают огонь и приседают, следующий код НЕ БУДЕТ работать. Это сработает, если им удастся нажать две клавиши в одно и то же время, но если частично (менее чем на полсекунды), этого не произойдет:

```c
if ((newkeys & KEY_FIRE) && !(oldkeys & KEY_FIRE) && (newkeys & KEY_CROUCH) && !(oldkeys & KEY_CROUCH))
```

Почему нет? Потому что OnPlayerKeyStateChange вызывается каждый раз при изменении одной клавиши. Поэтому при нажатии «KEY_FIRE» - OnPlayerKeyStateChange вызывается с «KEY_FIRE» в «newkeys», а не в «oldkeys», затем нажимается «KEY_CROUCH» - OnPlayerKeyStateChange вызывается с «KEY_CROUCH» и «KEY_FIRE» в «newkeys». «KEY_FIRE» теперь также находится в "oldkeys", поскольку он уже был нажат, поэтому "!(Oldkeys & KEY_FIRE)" завершится ошибкой. К счастью, решение очень простое (на самом деле проще, чем исходный код):

```c
if ((newkeys & (KEY_FIRE | KEY_CROUCH)) == (KEY_FIRE | KEY_CROUCH) && (oldkeys & (KEY_FIRE | KEY_CROUCH)) != (KEY_FIRE | KEY_CROUCH))
```

Это может показаться сложным, но он проверяет, что оба ключа установлены в "newkeys" и что оба ключа не были установлены в "oldkeys", если один из них был установлен в "oldkeys", это не имеет значения, поскольку оба ключа не имеют значения. Все это можно значительно упростить с помощью определений.

## Упрощение

### Обнаружение удержания клавиши

Определение:

```c
// HOLDING(keys)
#define HOLDING(%0) \
	((newkeys & (%0)) == (%0))
```

Удерживая одну клавишу:

```c
if (HOLDING( KEY_FIRE ))
```

Удержание нескольких клавиш:

```c
if (HOLDING( KEY_FIRE | KEY_CROUCH ))
```

### Обнаружение первого нажатия клавиши

Определение:

```c
// PRESSED(keys)
#define PRESSED(%0) \
	(((newkeys & (%0)) == (%0)) && ((oldkeys & (%0)) != (%0)))
```

Нажата одна клавиша:

```c
if (PRESSED( KEY_FIRE ))
```

Нажаты несколько клавиш:

```c
if (PRESSED( KEY_FIRE | KEY_CROUCH ))
```

### Обнаружение, если игрок нажимает клавишу в данный момент

Определение:

```c
// PRESSING(keyVariable, keys)
#define PRESSING(%0,%1) \
	(%0 & (%1))
```

Нажатие одной клавиши:

```c
if (PRESSING( newkeys, KEY_FIRE ))
```

Нажатие нескольких клавиш:

```c
if (PRESSING( newkeys, KEY_FIRE | KEY_CROUCH ))
```

### Обнаружение отпускания клавиши

Определение:

```c
// RELEASED(keys)
#define RELEASED(%0) \
	(((newkeys & (%0)) != (%0)) && ((oldkeys & (%0)) == (%0)))
```

Отпускание одной клавиши:

```c
if (RELEASED( KEY_FIRE ))
```

Отпускание нескольких клавиш:

```c
if (RELEASED( KEY_FIRE | KEY_CROUCH ))
```

## Примеры

### Прикрепите NOS, когда игрок нажимает огонь

```c
public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
	if (PRESSED(KEY_FIRE))
	{
		if (IsPlayerInAnyVehicle(playerid))
		{
			AddVehicleComponent(GetPlayerVehicleID(playerid), 1010);
		}
	}
	return 1;
}
```

### Супер прыжок

```c
public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
	if (PRESSED(KEY_JUMP))
	{
		new
			Float:x,
			Float:y,
			Float:z;
		GetPlayerPos(playerid, x, y, z);
		SetPlayerPos(playerid, x, y, z + 10.0);
	}
	return 1;
}
```

### Режим бога при удержании клавиши использования

```c
new
	Float:gPlayerHealth[MAX_PLAYERS];

#if !defined INFINITY
	#define INFINITY (Float:0x7F800000)
#endif

public OnPlayerKeyStateChange(playerid, newkeys, oldkeys)
{
	if (PRESSED(KEY_ACTION))
	{
		// Просто нажата клавиша действия, сохраните
		// старое здоровье для восстановления.
		GetPlayerHealth(playerid, gPlayerHealth[playerid]);
		SetPlayerHealth(playerid, INFINITY);
	}
	else if (RELEASED(KEY_ACTION))
	{
		// Отпускает действие - восстанавливаем
		// старое здоровье снова.
		SetPlayerHealth(playerid, gPlayerHealth[playerid]);
	}
	return 1;
}
```

### Объяснение

Вам не нужно беспокоиться о том, КАК это делается, просто так оно и есть. `HOLDING` определяет, нажимают ли они клавишу (или клавиши), независимо от того, нажимали ли они ее раньше, `PRESSED` обнаруживает, только что нажали ли они клавишу(-и), а `RELEASED` обнаруживает, только что отпущенную клавишу(-и). Однако если вы хотите узнать больше - читайте дальше.

Причина, по которой вам нужно делать это таким образом, а не просто использовать & или ==, заключается в том, чтобы точно определять нужные вам клавиши, игнорируя другие, которые могут или не могут быть нажаты. В двоичном формате `KEY_SPRINT`:

```
0b00001000
```

клавиша KEY_JUMP это:

```
0b00100000
```

таким образом, объединяя их в нужные ключи (мы также могли бы добавить их в этом примере, но это не всегда так) дает:

```
0b00101000
```

Если бы мы использовали только & и OnPlayerKeyStateChange вызывали для игрока, нажимающего прыжок, мы бы получили следующий код:

```
newkeys = 0b00100000
wanted  = 0b00101000
ANDed   = 0b00100000
```

AND двух чисел не равно 0, поэтому результат проверки верен, чего мы не хотим.

Если бы мы использовали только ==, два числа явно не совпадают, поэтому проверка не удалась бы, что мы и хотим.

Если бы игрок нажимал кнопку прыжка, спринта и приседания, мы получили бы следующий код:

```
newkeys = 0b00101010
wanted  = 0b00101000
ANDed   = 0b00101000
```

Версия с AND совпадает с требуемыми ключами, а также не 0, поэтому даст правильный ответ, однако два исходных числа не совпадают, поэтому == не удастся. В обоих примерах один из двух дал правильный ответ, а другой - неправильный. Если мы сравним первый, используя & и ==, мы получим:

```
newkeys = 0b00100000
wanted  = 0b00101000
ANDed   = 0b00100000
```

Очевидно, что желаемый и AND не одно и то же, поэтому проверка не выполняется, и это правильно. Для второго примера:

```
newkeys = 0b00101010
wanted  = 0b00101000
ANDed   = 0b00101000
```

Wanted и AND - это одно и то же, поэтому сравнение их как равных приведет к истинному результату, который снова является правильным.

Таким образом, используя этот метод, мы можем точно проверить, нажаты ли определенные клавиши, игнорируя все другие клавиши, которые могут или не могут быть нажаты. Проверка старых клавиш просто использует `!=` вместо `==`, чтобы убедиться, что требуемые клавиши не были ранее нажаты, поэтому мы знаем, что одна из них была только что нажата.