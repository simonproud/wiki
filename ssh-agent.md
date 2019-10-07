

## Windows
### Подготовка и настройка
Требуются
- GitBash
- OpenSSH

На локальной машине пишем
```
ssh-keygen -t rsa -b 4096 -C "<GitHub email>"
```
- отвечаем на вопросы, сгенерируется 2 файла. 
по умолчанию это id_rsa и id_rsa.pub 
- Открываем .pub файл любым блокнотом, копируем содержимое, идём на https://github.com/settings/keys , жмём New SSH Key, вводии тайтл и вставляем скопированное в тело. Сохраняем.
- Открываем папку с сохранёнными ключами, создаем файл "config", и добавляем содержимое:
```
Host <host_alias>
User <username>
HostName <host>
ForwardAgent yes 
```
- меняем поля `<host_alias>`  на удобный алиас, `<username>` на пользователя ssh, `<host>` на адрес подключения.
- открываем GitBash, пишем:
```
ssh-copy-id -i <~/.ssh/id_rsa.pub> <user>@<host>
```
где  `<~/.ssh/id_rsa.pub>` путь к сгенерированному публичному ключу,
`<user>` - пользователь ssh, `<host>` - адрес подключения

После всего этого на локальной машине выполняем  
```
ssh -T git@github.com
```
Видим ответ: Hi `GitHub Name`! You've successfully authenticated, but GitHub does not provide shell access.

Готово.
### Использование:
```
 eval $(ssh-agent -s)
 ```
```
ssh-add <путь к id_rsa>
```
И наконец подключаемся:
```
ssh <host_alias>
```

### END
