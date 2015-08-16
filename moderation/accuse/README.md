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