﻿API Администратора		
==================		
		
1. [**Поддержка:**](#Поддержка)  		
  - [Получить список вопросов.](#Получить-список-вопросов)		
  - [Задать вопрос.](#Задать-вопрос)		
2. [**Модерация:**](#Модерация)  		
  - [Проверить забанен ли пользователь.](#Проверить-забанен-ли-пользователь)		
  - [Забанить пользователя.](#Забанить-пользователя)		
  - [Получить причину бана.](#Получить-причину-бана)		
  - [Получить список банов.](#Получить-список-банов)		
  - [Отменить бан.](#Отменить-бан)		
		
## Поддержка		
		
#### Получить список вопросов:		
#####URL:[`/api/support/list`](http://funstream.tv/api/support/list)  		
**запрос:**		
```js		
{		
    category: <int|null>, //"Идентификатор категории."		
    from: <int|null>, //"Дата начала поиска (Юникс формат)."		
    onlyActive: <bool|null> //"Вернуть только активные вопросы(без ответов), true по умолчанию."		
}		
```		
**ответ<sup>1</sup>:**		
```		
[		
    ...,		
    {... /support/ask request ...},		
    ...		
]		
```		
<sup>1</sup>вернет ошибку если нет прав или неверная категория.		
		
#### Задать вопрос:  		
#####URL:[`/api/support/ask`](http://funstream.tv/api/support/ask)  		
**запрос:**		
```js		
{		
    category: <int>, //"Идентификатор категории."		
    question: <string> //"Текст вопроса."		
}		
```		
**ответ:**		
```js		
{		
    id: <int>, //"Идентификатор вопроса."		
    time: <string>, //"Дата и время вопроса(Юникс формат)."		
    category: <obj> {/*"... Те же данные, что и  /stream/category API запрос, без опций..."*/},		
    question: <string>, //"Текст вопроса."		
    active: <bool> //"true если нет ответа."		
}		
```		
		
## Модерация		
		
####  Проверить забанен ли пользователь:  		
#####URL:[`/api/moderation/check`](http://funstream.tv/api/moderation/check)  		
**запрос:**		
```js		
{		
    userId: <int> //"Идентификатор пользователя, которого нужно проверить."		
}		
```		
**ответ:**		
```js		
{		
    banned: <bool>, //"true если забанен, false если не забанен или пользователь не существует."		
    expire: <int> //"Время истечения бана или 0 если не забанен."		
}		
```		
*Если банов несколько, то вернет тот, который заканчивается позднее всего. Вернёт ошибку на пустой или 		
несуществующий `userId`.*		
		
#### Забанить пользователя:  		
#####URL:[`/api/moderation/accuse`](http://funstream.tv/api/moderation/accuse)  		
**запрос:**		
```js		
{		
    userId: <int>, //"Идентификатор пользователя, которого нужно попытаться забанить."		
    reasonId: <int>, //"Идентификатор причины бана."		
    data: <object|null> //"Дополнительная информация."		
}		
```		
*Ответ пустой, вернет ошибку если пользователь или причина не существует, либо если пользователь не залогинен.*		
		
#### Получить причину бана:		
#####URL:[`/api/moderation/reasons`](http://funstream.tv/api/moderation/reasons)		
**запрос:**		
```js		
{		
    content: <string> //"Содержание причины запрета, 'chat' по умолчанию."		
}		
```		
 		
**ответ:**		
```js		
[		
    ...,		
    {		
        id: <int>, //"Идентификатор причины."		
        name: <string>, //"имя причины."		
        content: <string> //"Содержание причины."		
    }		
    ...,		
]		
```		
		
#### Получить список банов:		
#####URL:[`/api/moderation/list`](http://funstream.tv/api/moderation/list)		
**запрос:**		
```js		
{		
    from: <int|null>, //"От временной метки."		
    to: <int|null>, //"До временной метки."		
    reason: <int|null> //"Фильтр по указанной причине."		
}		
```		
**ответ:**		
```js		
[		
    ...,		
    {		
        id: <int>, //"Идентификатор бана."		
        start: <int>, //"Время начала бана, временная метка."		
        end: <int>, //"Время истечения бана, временная метка."		
        reason: <obj> //"То же самое, что и /api/moderation/reasons объект"		
    }		
    ...,		
]		
```		
 		
#### Отменить бан:		
#####URL:[`/api/moderation/undo`](http://funstream.tv/api/moderation/undo)		
**запрос:**		
```js		
{		
    ban: <int> //"Идентификатор бана"		
}		
```		
*Ответ пустой.*		
*Отменяет выбранный бан, при этом выдавая бан всем пользователям, которые его ставили.*		
*Ответ ошибка если пользователь не авторизован или не имеет прав модератора.*