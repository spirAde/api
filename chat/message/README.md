#### Сообщение:  
#####URL:[`/chat/message`](http://funstream.tv/api/chat/message)  
```js
{
    id: <int>, //"идентификатор сообщения."
    from: <obj> {
        id: <int>, //"идентификатор пользователя."
        name: <string> //"имя пользователя."
    },
    to: <obj|null>, //"user object, тоже самое что и from."
    channel: <int>, //"идентификатор канала."
    text: <string>, //"текст сообщения."
    time: <datetime> //"дата и время сообщения."
}
```
Приходит для всех сообщений в текущий канал пользователя. Если пользователь авторизован, то и для всех сообщений, адресованных текущему пользователю, для любого канала.
