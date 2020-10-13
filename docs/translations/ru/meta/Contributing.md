---
Заголовок: Свой вклад
Описание: Как внести свой вклад в документацию SA-MP Wiki и open.mp.
---

Эта документация открыта для всех, кто может вносить изменения! Все, что вам нужно — это учетная запись [GitHub] (https://github.com) и немного свободного времени. Вам даже не нужно знать Git, вы можете делать все это через веб-интерфейс!

Если вы хотите помочь с поддержкой определенного языка, откройте PR файл [`CODEOWNERS`] (https://github.com/openmultiplayer/wiki/tree/master/CODEOWNERS) и добавьте строку для каталога вашего языка с вашим именем пользователя.

## Редактирование контента

На каждой странице есть кнопка, которая переводит вас на страницу GitHub для редактирования:

!["Изменить эту страницу" присутствует на каждой вики-странице](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/edit-this-page.png?raw=true)

Например, щелкнув эту ссылку на [SetVehicleAngularVelocity](https://github.com/openmultiplayer/wiki/blob/master/docs/scripting/functions/SetVehicleAngularVelocity.md) вы попадете на [эту страницу](https://github.com/openmultiplayer/wiki/edit/master/docs/scripting/functions/SetVehicleAngularVelocity.md), которая предоставляет собой текстовый редактор для внесения изменений в файл (при условии, что вы вошли в систему на GitHub).

Внесите свои изменения и отправьте «Pull Request». Это означает, что редакторы Wiki и другие члены сообщества могут просмотреть ваше изменение, обсудить, нужны ли для него дополнительные изменения, а затем объединить его.

## Добавление нового контента

Добавление нового контента немного сложнее. Сделать это можно двумя способами:

### Интерфейс GitHub

При просмотре каталога на GitHub в правом верхнем углу списка файлов есть кнопка «Добавить файл»:

!["Кнопка Добавить файл"](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/add-new-file.png?raw=true)

Вы можете либо загрузить уже написанный и размеченный файл, либо написать его прямо в текстовом редакторе GitHub.

Файл _должен_ иметь расширение .md и содержать разметку GitHub. Дополнительные сведения о Markdown смотрите в [этом руководстве] (https://guides.github.com/features/mastering-markdown/).

Как только это будет сделано, нажмите «Предложить новый файл», и "Pull Request" откроется для просмотра.

### Git

Если вы хотите использовать Git, все, что вам нужно сделать, это клонировать репозиторий Wiki с помощью:

```sh
git clone https://github.com/openmultiplayer/wiki.git
```

Откройте его в своем любимом редакторе. Мы рекомендуем Visual Studio Code, так как в нем есть отличные инструменты для редактирования и форматирования файлов Markdown. Как видите, это написано с помощью Visual Studio Code!

![Предварительный просмотр разметки в Visual Studio Code](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/vscode.png?raw=true)

Я рекомендую два расширения, чтобы вам было удобнее:

- [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint) от David Anson - это расширение, которое гарантирует, что ваш Markdown правильно отформатирован. Это предотвращает некоторые синтаксические и семантические ошибки. Не все предупреждения важны, но некоторые могут помочь улучшить читаемость. Используйте здравый смысл, а в случае сомнений просто спросите рецензента!
- [Prettier](https://marketplace.visualstudio.com/items?itemName=esbenp.prettier-vscode) от the Prettier.js Team - это средство форматирования, которое автоматически форматирует ваши файлы Markdown, чтобы все они использовали единый стиль. В репозитории Wiki есть некоторые настройки в файле `package.json`, которые расширение должно автоматически использовать. Обязательно включите "Форматировать при сохранении" в настройках редактора, чтобы ваши файлы Markdown автоматически форматировались при каждом сохранении!

## Примечания, советы и условные обозначения

### Внутренние ссылки

Не используйте абсолютные URL-адреса для межсайтовых ссылок. Используйте относительные пути.

- ❌

  ```md
  Для [OnPlayerClickPlayer] используется (https://www.open.mp/docs/scripting/callbacks/OnPlayerClickPlayer)
  ```

- ✔

  ```md
  Для [OnPlayerClickPlayer] используется (../callbacks/OnPlayerClickPlayer)
  ```

`../` означает «перейти на один каталог вверх», поэтому, если файл, который вы редактируете, находится внутри каталога `functions` и вы связываетесь с `обратными вызовами`, используйте `../` для перехода к `scripting /`, затем `callbacks / `для входа в каталог обратных вызовов, затем имя файла (без `.md`) обратного вызова, который вы хотите связать.

### Картинки

Изображения помещаются в подкаталог внутри `/ static / images`. Когда вы связываете изображение в `! [] ()`, просто используете `/ images /` в качестве базового пути (нет необходимости в `static`, только для репозитория).

Если сомневаетесь, прочтите другую страницу, где используются изображения и скопируйте правильное решение.

### Метаданные

Первым делом в _ любом_ документе должны быть метаданные:

```mdx
---
Заголовок: Моя документация
Описание: Это страница о всяких вещах и гамбургерах, ура!
---
```

Каждая страница должна включать заголовок и описание.

Полный список того, что может находиться между символами `---`, можно найти в [документации Docusaurus] (https://v2.docusaurus.io/docs/markdown-features#markdown-headers).

### Заголовки

Не создавайте заголовок 1 уровня (`<h1>`) с `#`, поскольку он создается автоматически. Ваш первый заголовок _всегда_ должен быть `##`

- ❌

  ```md
  # Мой заголовок

  Эта документация для...

  # Подраздел
  ```

- ✔

  ```md
  Эта документация для...

  ## Подраздел
  ```

### Используйте фрагменты кода для технических справок

При написании абзаца, содержащего имена функций, числа, выражения или что-либо, кроме стандартного письменного языка, окружайте их такими \`обратными кавычками \`. Это упрощает отделение языка описания вещей от ссылок на технические элементы, такие как имена функций и фрагменты кода.

- ❌

  > Функция fopen вернет значение с тегом типа File :, в этой строке нет проблем, поскольку возвращаемое значение сохраняется в переменной также с тегом File: (обратите внимание, случаи точно такие же). Однако в следующей строке к дескриптору файла добавляется значение 4. 4 не имеет тега [...]

- ✔

  > Функция `fopen` вернет значение с тегом типа `File:`, в этой строке нет проблем, поскольку возвращаемое значение сохраняется в переменной также с тегом `File:`(обратите внимание, случаи точно такие же). Однако в следующей строке к дескриптору файла добавляется значение «4». `4` не имеет тега [...]

В приведенном выше примере `fopen` - это имя функции, а не английское слово, поэтому окружение маркерами `code` помогает отличить его от другого содержимого.

Кроме того, если абзац относится к блоку кода примера, это помогает читателю связать слова с примером.

### Таблицы

Если в таблице есть заголовки, они идут в верхней части:

- ❌

  ```md
  |         |                                      |
  | ------- | ------------------------------------ |
  | Здоровье| Статус двигателя                     |
  | 650     | Неповрежденный                       |
  | 650-550 | Белый дым                            |
  | 550-390 | Серый дым                            |
  | 390-250 | Черный дым                           |
  | < 250   | Под огнем (совсем скоро взорвется)   |
  ```

- ✔

  ```md
  | Здоровье | Статус двигателя                     |
  | -------  | ------------------------------------ |
  | 650      | Неповрежденный                       |
  | 650-550  | Белый дым                            |
  | 550-390  | Серый дым                            |
  | 390-250  | Черный дым                           |
  | < 250    | Под огнем (совсем скоро взорвется)   |
  ```

## Переход с SA-MP Wiki

Большая часть контента была перемещена, но если вы обнаружите, что конкретная страница отсутствует, вот краткое руководство по преобразованию контента в Markdown.

### Получение HTML

1. Нажмите эту кнопку

   (Firefox)

   ![image](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/04f024579f8d.png?raw=true)

   (Chrome)

   ![image](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/f62bb8112543.png?raw=true)

2. Наведите указатель мыши на верхний левый угол главной страницы вики, пока не увидите `#content`

   ![image](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/65761ffbc429.png?raw=true)

   Или введите в поиске `<div id=content>`

3. Скопируйте внутренний HTML-код этого элемента

   ![image](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/8c7c75cfabad.png?raw=true)

  Теперь у вас есть _только_ HTML-код фактического _содержания_ страницы, то, что нам важно. Сейчас вы можете преобразовать его в Markdown.

### Преобразование HTML в Markdown

Для преобразования базового HTML (без таблиц) в Markdown используйте:

https://domchristie.github.io/turndown/

![image](https://github.com/openmultiplayer/wiki/blob/master/static/images/contributing/77f4ea555bbb.png?raw=true)

### Таблицы HTML в таблицы Markdown

Поскольку указанный выше инструмент не поддерживает таблицы, используйте этот инструмент:

https://jmalarcon.github.io/markdowntables/

И скопируйте только элемент `<table>`

### Очистка

Скорее всего, преобразование не будет идеальным. Так что вам придется немного отредактировать вручную. Перечисленные выше расширения форматирования должны помочь в этом, но вам все равно может потребоваться некоторое время на ручную работу.

Если у вас нет времени, не волнуйтесь! Отправьте незаконченный черновик, и кто-то другой сможет продолжить с того места, где вы остановились!

## Лицензионное соглашение

Все проекты open.mp имеют [Лицензионное соглашение участника][https://cla-assistant.io/openmultiplayer/homepage]. Это в основном означает, что вы соглашаетесь позволить нам использовать вашу работу и размещать ее под лицензией с открытым исходным кодом. Когда вы открываете "Pull Request" в первый раз, бот CLA-Assistant размещает ссылку, по которой вы можете подписать соглашение.