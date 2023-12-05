#### {"title": "Документация Alina API", "ignoreList": false}
# Документация по Alina API [alpha version]
## Доступные адреса
> [https://simplykel.ru/api/](https://simplykel.ru/api/) Через сайт <br>
> [https://api.simplykel.ru/](https://api.simplykel.ru/) Напрямую

## Безопастность некоторых функции
Некоторые знают что мой API не ограничивается на скинах & плащах. Есть функции которые используют доп. защиту в виде токена.<br>
Поэтому такие функции заблокированы на основе токена.
> Добавив параметр token и укажем верный токен, то мы получим результат уже от функции

## [all] /skin
Скины, скины и еще раз скины. Если бы не скины и привычка рытся в файлах модов, то этого апи не было бы.

### - [all] /configs/api.skins.json
> Список сервисов/API для получение скинов

> Сами посмотрите json, не маленькие<br>
> Просто перечислю какие используются в API

```
[0] Local files - Локальные файлы API
[1] Mojang API - Лицензионные скины
[2] ElyBy API
[3] SkinMe API
[4] LittleSkin - Использует формат SkinMe
[5] BlessingSkin - Использует формат SkinMe
[6] GlitchlessGames - Российский игровой сервис?
[7] RevolutionWorlds API - Приватный Minecraft Сервер
```

### - [all] /skin/render
> Параметры
```
name: Никнейм игрока
head: Сгенерировать голову
api: ID API сервиса
slim: Тонкие руки
sendfile: Отправка сразу файлом
```
### [GET] https://api.simplykel.ru/skin/render?name=Simply_Kel&api=2&head=false&sendfile=false
```JSON
{
    "nickname": "Simply_Kel",
    "skin": "http://ely.by/minecraft/skins/ad26dfb91be448e47225955a19ae7786.png",
    "model": "slim",
    "api": {
        "id": 2,
        "name": "ElyBy API",
        "type": 2,
        "root": "http://skinsystem.ely.by/textures/%PLAYER%",
        "icon": "https://ely.by/favicon.ico"
    },
    "file": {
        "local": "/root/alina-api/cache/skins/Simply_Kel-2.png",
        "web": "https://api.simplykel.ru/skins/Simply_Kel-2.png"
    },
    "render": {
        "local": "/root/alina-api/cache/renders/Simply_Kel-2-body.png",
        "web": "https://api.simplykel.ru/renders/Simply_Kel-2-body.png"
    }
}
```
### - [all] /skin/render/avatar
> Параметры
```
name: Никнейм игрока
api: ID API сервиса
two: Рендер второго слоя
sendfile: Отправка сразу файлом
```
### [GET] https://api.simplykel.ru/skin/render/avatar?name=Simply_Kel&api=2&sendfile=false&two=true
```JSON
{
     "nickname": "Simply_Kel",
     "skin": "http://ely.by/minecraft/skins/ad26dfb91be448e47225955a19ae7786.png",
     "model": "slim",
     "api": {
         "id": 2,
         "name": "ElyBy API",
         "type": 2,
         "root": "http://skinsystem.ely.by/textures/%PLAYER%",
         "icon": "https://ely.by/favicon.ico"
     },
     "file": {
         "local": "/root/alina-api/cache/skins/Simply_Kel-2.png",
         "web": "https://api.simplykel.ru/skins/Simply_Kel-2.png"
     },
     "render": {
         "local": "/root/alina-api/cache/renders/Simply_Kel-2-avatar.png",
         "web": "https://api.simplykel.ru/renders/Simply_Kel-2-avatar.png"
     }
}
```
## [all] /cape
### - [GET] /cape/render
> Параметры
```
name: Никнейм игрока
head: Сгенерировать голову
api: ID API сервиса
slim: Тонкие руки
sendfile: Отправка сразу файлом
```
### [GET] https://api.simplykel.ru/cape/render?name=Alexey&api=0&sendfile=false
```JSON
{
    "nickname": "Alexey",
    "cape": "http://textures.minecraft.net/texture/2340c0e03dd24a11b15a8b33c2a7e9e32abb2051b2481d0ba7defd635ca7a933",
    "api": {
        "id": 0,
        "name": "Minecraft",
        "type": 1,
        "urls": {
            "getInfo": "https://sessionserver.mojang.com/session/minecraft/profile/"
        }
    },
    "file": {
        "local": "/root/alina-api/cache/capes/Alexey-0.png",
        "web": "https://api.simplykel.ru/capes/Alexey-0.png"
    },
    "render": {
        "local": "/root/alina-api/cache/capesRenders/Alexey-0.png",
        "web": "https://api.simplykel.ru/cache/capesRenders/Alexey-0.png"
    }
}
```
##  Формат ошибок
### [GET] https://api.simplykel.ru/amogus2281337
```json
{
    "error": {
        "code": 404,
        "codename": "Not found",
        "message": "Method not found"
    }
}
```
