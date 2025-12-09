Проект Wiki JS (emptyDir и nodePort)
---

Содержащиеся в проекте манифесты поднимают 2 сервиса и 2 пода соответственно:
1. С веб-приложением Wiki JS
2. С базой данных PostgreSQL

Сеть
---
Сетевое взаимодействие подов реализовано через ClusterIP.
Для пода Wiki JS реализован nodePort по порту **30123**.

Deploy
---
Приложение разворачивается через команду (находясь в директории проекта)
```kubectl apply -f deploy/```

Проверка работы приложения
---
>Для способов 2, 3, 4 необходимо узнать, на какой ноде поднят под с приложением.
Сделать это можно с помощью команды
```kubectl get pods -o wide | grep "wikijs-*"```.

Способы проверки работы приложения:
1. Подключившись к поду приложения: ```kubectl exec -it deployment/wikijs -- curl -v http://localhost:3000```
2. Если есть такая возможность, то подключиться к ноде по ssh и проверить командной ```curl -v http://localhost:30123```
3. Если нода в вашей сети, то через браузер по адресу http://<ip_node>:30123
4. Если нода находится за NAT, то необходимо настроить проброс порта c хоста, например 8080, на порт 30123 ноды, а после открыть в браузере хоста адрес http://localhost:8080
---
**Как понять, что приложение работает?**

Если вы использовали способ с проверкой через браузер, то вы увидете страницу с регистрацией администратора приложения. Можете зарегистрироваться и дальше взаимодействовать с приложением.

Если вы использовали способ с командой *curl*, то вы должны увидеть подобный вывод:

```<!DOCTYPE html>
<html lang="en"><head><meta http-equiv="X-UA-Compatible" content="IE=edge"><meta charset="UTF-8"><meta name="viewport" content="user-scalable=yes, width=device-width, initial-scale=1, maximum-scale=5"><meta name="theme-color" content="#1976d2"><meta name="msapplication-TileColor" content="#1976d2"><meta name="msapplication-TileImage" content="/_assets/favicons/mstile-150x150.png"><title>Welcome | Wiki.js</title><meta name="description"><meta property="og:title" content="Welcome"><meta property="og:type" content="website"><meta property="og:description"><meta property="og:image"><meta property="og:url" content="https://wiki.yourdomain.com/"><meta property="og:site_name" content="Wiki.js"><link rel="apple-touch-icon" sizes="180x180" href="/_assets/favicons/apple-touch-icon.png"><link rel="icon" type="image/png" sizes="192x192" href="/_assets/favicons/android-chrome-192x192.png"><link rel="icon" type="image/png" sizes="32x32" href="/_assets/favicons/favicon-32x32.png"><link rel="icon" type="image/png" sizes="16x16" href="/_assets/favicons/favicon-16x16.png"><link rel="mask-icon" href="/_assets/favicons/safari-pinned-tab.svg" color="#1976d2"><link rel="manifest" href="/_assets/manifest.json"><script>var siteConfig = {"title":"Wiki.js","theme":"default","darkMode":false,"tocPosition":"left","lang":"en","rtl":false,"company":"","contentLicense":"","footerOverride":"","logoUrl":"https://static.requarks.io/logo/wikijs-butterfly.svg"}
var siteLangs = []
</script><link type="text/css" rel="stylesheet" href="/_assets/css/app.2144b7acef37b4a5cc2e.css"><script type="text/javascript" src="/_assets/js/runtime.js?1755069093"></script><script type="text/javascript" src="/_assets/js/app.js?1755069093"></script></head><body><div class="is-fullscreen" id="root"><welcome locale="en"></welcome></div></body></html>```