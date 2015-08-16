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
*Ответ ошибка если пользователь API не авторизован или не имеет привилегий модератора. Привилегии можно проверить вызовом `/api/user/current`.*