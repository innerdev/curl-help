Слайд 1. Что такое CURL?
========================

cURL — (распространяемая по лицензии MIT), кроссплатформенная служебная программа командной строки, позволяющая взаимодействовать с множеством различных серверов по множеству различных протоколов с синтаксисом URL.

Название произошло от "Client for URLs". Замечу, что URL - по сути это ссылка. Это некий адрес в сети Интернет. Например http://yandex.ru/search - является URL.

Подробнее можно почитать тут: https://ru.wikipedia.org/wiki/URL

Главное, что нужно отметить из определения на данный момент, тот факт, что CURL - это программа. По-простому - "экзешник" (для Windows). Просто обычная программа. Точно такая же, как Word или Photoshop, но которую запустить, впрочем, можно только из консоли или, как еще называют, интерфейса командной строки или просто из командной строки.

Чтобы лучше познакомиться с консолью, рекомендуется прочитать: https://ru.wikipedia.org/wiki/%D0%98%D0%BD%D1%82%D0%B5%D1%80%D1%84%D0%B5%D0%B9%D1%81_%D0%BA%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%BD%D0%BE%D0%B9_%D1%81%D1%82%D1%80%D0%BE%D0%BA%D0%B8

Оригинальным автором CURL является Дэниел Стенберг (Daniel Stenberg).

Включена в состав Windows 10 с 2018 года (обновление  Redstone 4 April 2018 Update).

Чем нам это важно? Тем, что программа кросс-платформенная (то есть на 2021 год имеется на любых операционных системах) и позволяет запрашивать множество протоколов, а именно: FTP, FTPS, HTTP, HTTPS, TFTP, SCP, SFTP, Telnet, DICT, LDAP, а также POP3, IMAP и SMTP. Также cURL поддерживает сертификаты HTTPS, методы HTTP POST, HTTP PUT, загрузку на FTP, загрузку через формы HTTP.

Нам, в данном случае, скорее всего важны только HTTP и HTTPS.

Сразу оговорюсь, что сейчас и далее под словом "сервер" иногда имеется ввиду физический компьютер, который стоит в стойке какого-то дата-центра и просто работает. Но почти всегда все же имеется ввиду программа, которая бесконечно "висит" в памяти этого компьютера и просто ожидает запрос, на который реагирует каким-то образом и возвращает какой-то ответ. Первое обычно называется "аппаратным обеспечением", а второе "программным обеспечением".

Почитать подробнее про сервера можно тут:

Аппаратное обеспечение: https://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%80%D0%B2%D0%B5%D1%80_(%D0%B0%D0%BF%D0%BF%D0%B0%D1%80%D0%B0%D1%82%D0%BD%D0%BE%D0%B5_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5)

Программное обеспечение: https://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%80%D0%B2%D0%B5%D1%80_(%D0%BF%D1%80%D0%BE%D0%B3%D1%80%D0%B0%D0%BC%D0%BC%D0%BD%D0%BE%D0%B5_%D0%BE%D0%B1%D0%B5%D1%81%D0%BF%D0%B5%D1%87%D0%B5%D0%BD%D0%B8%D0%B5)

Кроме того, чтобы лучше понимать происходящее, рекомендую почитать про клиент и сервер: https://ru.wikipedia.org/wiki/%D0%9A%D0%BB%D0%B8%D0%B5%D0%BD%D1%82_%E2%80%94_%D1%81%D0%B5%D1%80%D0%B2%D0%B5%D1%80

В двух словах, клиентом обычно называется программа, делающая запрос, а сервером - обрабатывающая запрос. Например, компьютерные игры. Когда мы играем в массовую мультиплеерную компьютерную игру, то программа на вашем компьютере (WoW / CSGO / Dota и т.п.) является клиентом. И она подключается к серверу. Сервер обрабатывает данные от каждой подключенной программы (например, перемещение игрока) и в качестве полезной работы, в частности, рассылает эти данные всем остальным игрокам. Кроме того, может выполнять и другие функции, например, фиксирование факта попадания мечом или пулей одного игрока в другого и рассылать эти данные всем остальным игрокам, чтобы они увидели это в своих клиентах (в игре).

В играх, как правило, всё немножко иначе, чем у нас с API. У нас обычно происходит так называемый "запрос-ответ", когда мы не имеем состояния (такого, как здоровье, позиция игрока), тем не менее, мы точно так же делаем запросы и получаем ответы от сервера. Можно применить эту аналогию и дальше: например, если бы мы писали компьютерную игру, мы бы постоянно делали запрос о том, где находятся враги и сколько у них здоровья, а сервер постоянно отвечал бы нам, присылая данные об этом. Таким образом, клиент (игра на компьютере пользователя) всегда была бы в курсе, где находятся другие игроки.

В нашем же случае, обычно, мы запрашиваем не положение игроков, а какие-то данные. Например, цены на товары. Как правило, цены на товары не меняются с такой же скоростью, как позиции игроков в игре, поэтому для нас запросы и ответы выглядят куда более "стабильными" и не меняющимися с течением времени. Уверен, станет понятнее после прочтения статьи до конца.


Слайд 2. Что такое HTTP? Напоминалка.
=====================================

HTTP (англ. HyperText Transfer Protocol — «протокол передачи гипертекста») — протокол прикладного уровня передачи данных, изначально — в виде гипертекстовых документов в формате HTML, в настоящее время используется для передачи произвольных данных.

"Протокол прикладного уровня" означает, что наши системы обмена данными, такие как REST или SOAP, строятся поверх него и используют его для передачи данных.

Например, когда вы запрашиваете URL в виде https://domain.com/users/6 - вы получаете данные по конкретному пользователю через REST, но при этом данные вам приходят по протоколу HTTP. Когда вы отправляете XML-документ для SOAP по адресу https://shop.com/ - вы тоже используете HTTP.

Чтобы понять лучше, можно посмотреть на сетевую модель OSI: https://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%B0%D1%8F_%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C_OSI

Как видно из приведенной схемы, протокол прикладного уровня - самый "верхний", именно с ним мы и работаем посредством CURL. REST или SOAP работают уже "поверх" этого протокола.

Ссылки для ознакомления с REST и SOAP, рекомендуется прочитать для понимания:

https://ru.wikipedia.org/wiki/REST

https://ru.wikipedia.org/wiki/SOAP

Слайд 3. Что надо знать про HTTP для CURL.
==========================================

Тут нужно понимать, что такое тип запроса (он же - метод запроса) в HTTP.
Почитать продробнее можно тут: https://ru.wikipedia.org/wiki/HTTP#%D0%9C%D0%B5%D1%82%D0%BE%D0%B4%D1%8B

Сейчас остановимся на том, что при отправке запроса через HTTP мы указываем, что именно мы хотим сделать. Например - получить данные. Или записать данные. Таким образом серверное программное обеспечение "поймет" нас правильно.

Для примера: когда в браузере вы открываете сайт, вы выполняете так называемый GET-запрос (здесь метод - это GET). Посылая такой запрос, сервер знает, что он должен прислать вам html-код сайта, который отобразится в браузере. Метод так и называется - GET. Получить.

Также нужно знать, что такое код ответа или код состояния. Когда сервер присылает вам данные, он также присылает код ответа. Это целое трехзначное число. Кодов ответа существует большое множество, ознакомиться с ними подробнее можно по этим ссылкам:

https://ru.wikipedia.org/wiki/HTTP#%D0%9A%D0%BE%D0%B4%D1%8B_%D1%81%D0%BE%D1%81%D1%82%D0%BE%D1%8F%D0%BD%D0%B8%D1%8F

https://ru.wikipedia.org/wiki/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BA%D0%BE%D0%B4%D0%BE%D0%B2_%D1%81%D0%BE%D1%81%D1%82%D0%BE%D1%8F%D0%BD%D0%B8%D1%8F_HTTP

На практике обычно мы должны знать несколько кодов ответа. Например, код 200 означает, что всё хорошо. А вот код 500 означает, что на сервере возникла проблема и данные нам не придут (в нашем примере - не придет html-код сайта и сайт не отобразится). В браузере это часто дружелюбно выглядит как "что-то пошло не так" или похожие страницы с ошибками.

Слайд 4. Первый GET-запрос через CURL.
===============================

Чтобы сделать свой первый запрос через CURL, необходимо открыть консоль (cmd или powershell в windows 10). И вписать следующую команду:

```
curl https://www.google.com
```

В результате работы программы CURL (и выполнения этой команды) вы увидите что-то вроде этого:

```
>curl https://www.google.com
<!doctype html><html itemscope="" itemtype="http://schema.org/WebPage" lang="ru"><head><meta content="&#1055;&#10...
```

Мы сделали GET-запрос в Google. Сервер понял его как "нужно отдать HTML-код сайта" и на выходе мы получили HTML-код страницы https://www.google.com/

Замечу, что если вы сделаете запрос к адресу https://google.com, то сервер пришлет вам другой html-код:

```
>curl https://google.com
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
```

Как видно из текста, нам пришел статус 301 (об этом ниже) и текст о том, что адрес сайта на самом деле другой, а именно www.google.com (обратите внимение на www в начале).


Слайд 5. Отображение статусов.
==============================

Как видно из примера выше, где мы отправили GET-запрос на адрес www.google.com, мы получили HTML-код сайта. Но где же находятся коды ответов и заголовки запроса?

Что такое заголовки, можно почитать вот тут: https://ru.wikipedia.org/wiki/HTTP#%D0%97%D0%B0%D0%B3%D0%BE%D0%BB%D0%BE%D0%B2%D0%BA%D0%B8

Чтобы отобразить коды состояния, нам необходимо дописать так называемый флаг в нашу команду. Флаги также можно назвать "опцией". Мы дополнительно указываем программе, что она должна сделать что-то дополнительно или по-другому. Давайте сделаем такой запрос. Нам понадобится флаг "-I" (без кавычек):

```
>curl -I https://www.google.com
HTTP/1.1 200 OK
Content-Type: text/html; charset=ISO-8859-1
...
```

Здесь нас интересует строка "HTTP/1.1 200 OK". Это и есть статус ответа (статус код). В данном случае он 200, что означает, что запрос успешно принят, обработан и ответ отдан клиенту (в данном случае - программе CURL; из примеров выше можно понять, что это мог бы быть и браузер).

Давайте попробуем сделать такой же запрос, но к google.com, без WWW:

```
>curl -I https://google.com
HTTP/1.1 301 Moved Permanently
Location: https://www.google.com/
...
```

Здесь статус-код уже другой, а именно - 301. Этот статус означает, что страница изменила свой URL (местоположение, адрес) и по полю Location мы можем понять, где именно она теперь находится. В просторечье это называется "редирект". Перенаправление пользователя с одного адреса на другой. Например, если ваш браузер примет такой запрос (с кодом 301), он автоматически перейдет на страницу, указанную в поле Location. Кстати, Location в данном случае - это заголовок запроса.


Слайд 6. Заголовки запроса.
===========================

Наконец-то скажу, что HTTP-запрос - это просто текст. В этом нет никакой магии. Когда вы отправляете запрос, вы отправляете текст. Когда вы получаете ответ от сервера - вы получаете текст. Ничего страшного внутри запроса нет.

Пример запроса для регистрации пользователя в одном из моих приложений:

```
POST https://domain.com/api/register
Content-Type: application/json

{"name": "Dmitry", "email": "test@test.com", "password":  "mysuperpassword123"}
```

Весь HTTP-запрос можно поделить на несколько секций, почти все из них тут присутствуют. А именно:

* Стартовая строка. Она содержит метод запроса (GET, POST и другие) и URL, куда мы хотим обратиться. 

* Заголовки запроса. Заголовоки запроса это строки в HTTP-сообщении, содержащие разделённую двоеточием пару параметр-значение. В данном случае мы сообщаем серверу, что тип контента, который мы отправляем в теле сообщения (см. ниже) содержит JSON.

Сноска: чтобы узнать, что такое JSON, можно почитать вот тут: https://ru.wikipedia.org/wiki/JSON

* Тело сообщения: это полезная информация (в виде текста), которую мы хотим передать на сервер.

В частности отмечу, что заголовки от тела запроса отделены пустой строкой, поэтому в примере выше пустая строка - не ошибка, это всё еще часть "договоренности" для HTTP-запросов.

* Код запроса. Мы уже обсудили это выше, но отмечу, что код запроса не нужен, если мы делаем запрос на сервер. Код (или статус запроса) мы всегда только принимаем, т.к. мы являемся клиентом. Мы получаем его в ответе от сервера. Сервер просто сообщает нам, что что-то пошло не так, страница изменила адрес или всё прошло хорошо. И было бы странно отправлять код запроса серверу самостоятельно.

По аналогии с этим заголовки, на самом деле, делятся на заголовки запроса и заголовки ответа. Сервер часто может прислать нам какой-нибудь заголовок, который мы серверу никогда не отправляем. Проще всего это всё представить как общение людей: мы здороваемся с человеком и спрашиваем как у него дела, но не сообщаем ему о своих проблемах еще до слова "привет". При этом человек может ответить нам, что он занят и сейчас ему не до нас (по аналогии с кодом ответа 500, когда на сервере произошла ошибка при обработке нашего запроса).

Про заголовки запроса можно почитать вот тут: 
https://ru.wikipedia.org/wiki/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%B7%D0%B0%D0%B3%D0%BE%D0%BB%D0%BE%D0%B2%D0%BA%D0%BE%D0%B2_HTTP#%D0%9E%D1%81%D0%BD%D0%BE%D0%B2%D0%BD%D1%8B%D0%B5_%D0%B7%D0%B0%D0%B3%D0%BE%D0%BB%D0%BE%D0%B2%D0%BA%D0%B8

И вот тут: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers


Слайд 7. Сохранение результата запроса в файл.
=============================================

Чтобы сохранить ответ сервера, можно использовать флаг -o или -O (буква "O", английская, НЕ ноль):

```
>curl -o test.txt https://google.com
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100   220  100   220    0     0    220      0  0:00:01 --:--:--  0:00:01  2018
```

После выполнения этой команды HTTP-код страницы google.com будет скачан и сохранен в файл с названием test.txt. Это удобно, когда необходимо показать кому-то ответ или приложить его к задаче. В данном случе содержимое файла будет точно таким же, как мы видели выше (но до этого вывод был в консоль, а теперь в файл):

```
>more test.txt
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
```


Слайд 8. Добавление заголовков к запросу.
=========================================

Чтобы добавить заголовок к запросу, мы можем использовать флаг "-H" (без кавычек), следующим образом:

```
curl -H "X-Header: value" https://google.com
```

Где X-Header - это название заголовка, а value - это его значение. Позже будет понятнее, когда мы сделаем запрос с телом. В данном случае, если выполнить такой запрос, сайт google.com его просто не поймет и проигнорирует. Обработка заголовков (как и запроса в целом) - это прерогатива сервера. Фактически, мы не можем знать как сервер отреагирует на наш запрос, это его дело. Поэтому не удивляйтесь, если добавление дополнительных опций в ваших запросах не вызовет никакого нового поведения сервера.



Слайд 9. Получение полной информации об ответе сервера.
=======================================================

Когда мы делаем запрос, происходит много важной работы для того, чтобы клиент и сервер начали общаться друг с другом. Обычно она нам не нужна и даже не видна. Но если у нас что-то идет не так (например, мы делаем запрос, а получаем пустой ответ), мы можем попробовать вывести полную информацию о запросе с помощью добавления флага "-v" (без кавычек), например, вот так:

```
>curl -H "X-Header: value" https://google.com -v
* Rebuilt URL to: https://google.com/
*   Trying 142.250.150.100...
* TCP_NODELAY set
* Connected to google.com (142.250.150.100) port 443 (#0)
* schannel: SSL/TLS connection with google.com port 443 (step 1/3)
* schannel: checking server certificate revocation
* schannel: sending initial handshake data: sending 175 bytes...
* schannel: sent initial handshake data: sent 175 bytes
* schannel: SSL/TLS connection with google.com port 443 (step 2/3)
* schannel: failed to receive handshake, need more data
* schannel: SSL/TLS connection with google.com port 443 (step 2/3)
* schannel: encrypted data got 3759
* schannel: encrypted data buffer: offset 3759 length 4096
* schannel: sending next handshake data: sending 93 bytes...
* schannel: SSL/TLS connection with google.com port 443 (step 2/3)
* schannel: encrypted data got 292
* schannel: encrypted data buffer: offset 292 length 4096
* schannel: SSL/TLS handshake complete
* schannel: SSL/TLS connection with google.com port 443 (step 3/3)
* schannel: stored credential handle in session cache
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/7.55.1
> Accept: */*
> X-Header: value
>
* schannel: client wants to read 102400 bytes
* schannel: encdata_buffer resized 103424
* schannel: encrypted data buffer: offset 0 length 103424
* schannel: encrypted data got 737
* schannel: encrypted data buffer: offset 737 length 103424
* schannel: decrypted data length: 708
* schannel: decrypted data added: 708
* schannel: decrypted data cached: offset 708 length 102400
* schannel: encrypted data buffer: offset 0 length 103424
* schannel: decrypted data buffer: offset 708 length 102400
* schannel: schannel_recv cleanup
* schannel: decrypted data returned 708
* schannel: decrypted data buffer: offset 0 length 102400
< HTTP/1.1 301 Moved Permanently
< Location: https://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Date: Tue, 23 Mar 2021 12:32:35 GMT
< Expires: Thu, 22 Apr 2021 12:32:35 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 220
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< Alt-Svc: h3-29=":443"; ma=2592000,h3-T051=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"
<
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```

Здесь мы видим всю информацию, начиная с момента, когда URL преобразовывается к IP-адресу 142.250.150.100, после чего происходит подключение к порту 443 и так далее. Не будем останавливаться на этом подробно, т.к. здесь уже речь точно не про CURL и даже не совсем про HTTP.

Почитать, почему URL преобразовывается к IP-адресу можно тут: https://ru.wikipedia.org/wiki/DNS

Как работает HTTPS можно тут: https://ru.wikipedia.org/wiki/HTTPS

Про TCP/IP почитать можно тут: https://ru.wikipedia.org/wiki/TCP/IP

Про модель сети почитать можно тут: https://ru.wikipedia.org/wiki/%D0%A1%D0%B5%D1%82%D0%B5%D0%B2%D0%B0%D1%8F_%D0%BC%D0%BE%D0%B4%D0%B5%D0%BB%D1%8C_OSI


Слайд 10. Отображение тела ответа и заголовков одновременно.
============================================================

Очень полезной опцией является отображение тела запроса и заголовков ответа (включая код ответа) одновременно. Сделать это можно с помощью опции "-D -", следующим образом:

```
>curl -D - https://google.com
HTTP/1.1 301 Moved Permanently
Location: https://www.google.com/
Content-Type: text/html; charset=UTF-8
Date: Tue, 23 Mar 2021 12:38:07 GMT
Expires: Thu, 22 Apr 2021 12:38:07 GMT
Cache-Control: public, max-age=2592000
Server: gws
Content-Length: 220
X-XSS-Protection: 0
X-Frame-Options: SAMEORIGIN
Alt-Svc: h3-29=":443"; ma=2592000,h3-T051=":443"; ma=2592000,h3-Q050=":443"; ma=2592000,h3-Q046=":443"; ma=2592000,h3-Q043=":443"; ma=2592000,quic=":443"; ma=2592000; v="46,43"

<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="https://www.google.com/">here</A>.
</BODY></HTML>
```

В этом случае мы одновременно видим и тело ответа (HTML-код сайта) и заголовки/код ответа (301/Location). Напомню, что код 301 - это код ответа и он означает, что веб-страница изменила свой адрес. А Location - это заголовок, который указывает на новый адрес страницы. Также поясню, т.к. HTTP-сообщение может быть сформировано, в общем-то, любым образом, на практике вы можете получать код ответа и заголовок, не согласованные друг с другом. Например, код ответа 301 без заголовка Location и так далее. В таком случае получается, что серверное приложение, отправляющее вам ответ, не следует спецификации HTTP и остается только разбираться самостоятельно, что произошло и что делать в этом случае.

Мысль, которую я хотел бы донести в предыдущем абзаце: не всегда сервера написаны идеально. Иногда там могут быть сбои, ошибки или проблемы, которые заранее предугадать невозможно. И эта проблема ложится на плечи аналитиков, поэтому необходимо быть подготовленным и знать спецификацию если уж и не идеально, то хотя бы хорошо.


Слайд 11. Указание метода запроса.
==================================

Как было сказано выше, мы можем сделать не только GET-запрос, но и POST-запрос и другие возможные (PUT, PATCH, DELETE и др.). Чтобы указать тип запроса, выполните команду с флагом "--request" или "-X" (икс большая, без кавычек):

```
curl --request GET https://www.google.com/
```

или 

```
curl -X GET https://www.google.com/
```

В данном случае мы сделали все тот же GET-запрос, который делали и до этого. Поэтому результат будет тем же. Тем не менее, мы можем сделать и POST-запрос. Напомню, что POST-запросы нужны для отправки данных на сервер, а не для получения данных. Давайте сделаем этот запрос:

```
curl -X POST https://www.google.com/
```

Мы получаем довольно неожиданный ответ:

```
>curl -X POST https://www.google.com/
<!DOCTYPE html>
<html lang=en>
  <meta charset=utf-8>
  <meta name=viewport content="initial-scale=1, minimum-scale=1, width=device-width">
  <title>Error 411 (Length Required)!!1</title>
  <style>
    *{margin:0;padding:0}html,code{font:15px/22px arial,sans-serif}html{background:#fff;color:#222;padding:15px}body{margin:7% auto 0;max-width:390px;min-height:180px;padding:30px 0 15px}* > body{background:url(//www.google.com/images/errors/robot.png) 100% 5px no-repeat;padding-right:205px}p{margin:11px 0 22px;overflow:hidden}ins{color:#777;text-decoration:none}a img{border:0}@media screen and (max-width:772px){body{background:none;margin-top:0;max-width:none;padding-right:0}}#logo{background:url(//www.google.com/images/branding/googlelogo/1x/googlelogo_color_150x54dp.png) no-repeat;margin-left:-5px}@media only screen and (min-resolution:192dpi){#logo{background:url(//www.google.com/images/branding/googlelogo/2x/googlelogo_color_150x54dp.png) no-repeat 0% 0%/100% 100%;-moz-border-image:url(//www.google.com/images/branding/googlelogo/2x/googlelogo_color_150x54dp.png) 0}}@media only screen and (-webkit-min-device-pixel-ratio:2){#logo{background:url(//www.google.com/images/branding/googlelogo/2x/googlelogo_color_150x54dp.png) no-repeat;-webkit-background-size:100% 100%}}#logo{display:inline-block;height:54px;width:150px}
  </style>
  <a href=//www.google.com/><span id=logo aria-label=Google></span></a>
  <p><b>411.</b> <ins>ThatтАЩs an error.</ins>
  <p>POST requests require a <code>Content-length</code> header.  <ins>ThatтАЩs all we know.</ins>
```

Обратите внимание, сервер понял, что мы хотим отправить ему данные, но мы не отправили дополнительный необходимый заголовок запроса, чтобы сервер мог корректно обработать наш запрос (а именно заголовок "Content-length").

Сейчас мы не будем на этом останавливаться, рекомендуется обратиться к документации по HTTP.


Слайд 12. Отправка тела запроса.
================================

Чтобы отправить запрос с телом запроса, используйте флаг "-d" (без кавычек). Также можно использовать аналог этого флага: "--data" (без кавычек). Например, вот так:

```
curl -X POST http://www.yourwebsite.com/login/ -d 'username=yourusername&password=yourpassword'
```

Или 

```
curl -X POST http://www.yourwebsite.com/login/ --data 'username=yourusername&password=yourpassword'
```

Мы сделали POST-запрос и передали в качестве тела запроса две переменные, username и password. Замечу, что технически тело запроса может быть любым текстом. В данном случае мы передали переменные согласно спецификации протокола HTTP.

Подробнее про переменные (они же - параметры) можно почитать вот тут: https://ru.wikipedia.org/wiki/HTTP#GET

* ВНИМАНИЕ! Под Windows могут быть сложности с отправкой данных прямо в командной строке с помощью флага -d. Это связано, видимо, с особенностями работы терминала в Windows. Если у вас Windows, рекомендуется почитать про эту проблему, например, на stackoverflow: https://stackoverflow.com/questions/7172784/how-do-i-post-json-data-with-curl

Кроме того, можно отправлять данные из файла. Это удобно в случае, когда нужно в теле запроса отправить много текста и его неудобно редактировать прямо в консоли. Для этого нужно сделать следующий запрос:

```
curl -X POST -d @filename http://domain.com/resource
```

Где filename - это имя файла (вы должны находиться в каталоге, где есть этот файл, либо указать полный путь к нему).




Слайд 13. Пример запроса и ответа.
==================================

Завершая тему запросов и ответов в HTTP, хочется привести пример запроса и ответа из Wiki:

Запрос:

```
GET /wiki/страница HTTP/1.1
Host: ru.wikipedia.org
User-Agent: Mozilla/5.0 (X11; U; Linux i686; ru; rv:1.9b5) Gecko/2008050509 Firefox/3.0b5
Accept: text/html
Connection: close
(пустая строка)  
```

Ответ:

```
HTTP/1.1 200 OK
Date: Wed, 11 Feb 2009 11:20:59 GMT
Server: Apache
X-Powered-By: PHP/5.2.4-2ubuntu5wm1
Last-Modified: Wed, 11 Feb 2009 11:20:59 GMT
Content-Language: ru
Content-Type: text/html; charset=utf-8
Content-Length: 1234
Connection: close
(пустая строка)
(запрошенная страница в HTML)
```

Это общий вид запроса и ответа в HTTP. На данном этапе должно быть понятно, где находится статус (код) ответа, заголовки, тело запроса, тело ответа и тот факт, что они разделены пустой строкой.


Слайд 14. Пример запроса на регистрацию.
========================================

Давайте попробуем объединить наши знания и сделать запрос на регистрацию в одном из сервисов (это пример, для получения реальных данных см. ниже). На вход он принимает формат JSON, с полями name, email и password. Например, вот такого вида:

```
{"name": "Dima", "email": "test@test.com", "password":  "mypassword123"}
```

Давайте создадим файл с именем body.txt, запишем в него JSON из примера выше и сделаем запрос с использованием этого файла:

```
>curl -X POST -H "Content-Type: application/json" -d @body.txt http://domain.com/api/register
```

В качестве ответа, если сервер обработал наш запрос согласно спецификации, мы получим ответ об успехе, например:

```
{"success":true,"message":"\u0412\u044b \u0443\u0441\u043f\u0435\u0448\u043d\u043e \u0437\u0430\u0440\u0435\u0433\u0438\u0441\u0442\u0440\u0438\u0440\u043e\u0432\u0430\u043b\u0438\u0441\u044c.","data":{"token":"eyJ...XE"}}
```

Обращаю ваше внимание, что сообщение с сервером может быть в любом формате. Это не обязательно должен быть JSON, это может быть XML или собственный протокол (договоренность о том, как клиент должен общаться с сервером). Ответ сервера выше - это просто пример.


Слайд 15. Пример запроса в реальный RESTful-сервис.
==================================

Давайте попробуем сделать запрос в тестовый сервис с REST API. Сервис просто генерирует нам какие-то случайные данные и служит для тестирования. Согласно спецификации, мы можем сделать запрос на URL https://jsonplaceholder.typicode.com/todos и получить оттуда JSON с содержание списка TODO. Кроме того, это должен быть GET-запрос. Сделаем запрос, согласно этим данным (на самом деле "-X GET" можно не указывать, т.к. по умолчанию CURL делает именно GET-запрос, это сделано для понимания):

```
>curl -X GET https://jsonplaceholder.typicode.com/todos
```

И мы видим ответ, тоже в формате JSON:

```
[
  {
    "userId": 1,
    "id": 1,
    "title": "delectus aut autem",
    "completed": false
  },
  {
    "userId": 1,
    "id": 2,
    "title": "quis ut nam facilis et officia qui",
    "completed": false
  },
...
]
```

Попробуйте сделать этот запрос самостоятельно.


Слайд 16. Загрузка файлов.
==========================

Иногда мы должны отправить на сервер какой-то файл. Сейчас речь идет не про тело запроса, а, например, про загрузку аватарки в ВК или чего-то подобного. Например, мы хотим отправить на сервер файл с нашей фотографией, изображение в формате jpg. В таком случае мы должны использовать флаг "-F" (без кавычек) и выполнить следующую команду:

```
curl -X POST -F 'image=@C:\users\user\avatar.jpg' http://example.com/upload
```

Обращаю ваше внимание, что это POST-запрос. Это логично, т.к. мы хотим не получить данные (как в случае GET-запросов), а отправить данные.


Слайд 17. Дополнительные материалы.
===================================

В состав программы CURL входит встроенная помощь. Вызвать ее можно с помощью добавления флага "-h" (без кавычек) или "--help":

```
>curl --help
```

Вы получите краткую справку о программе и ее флагах прямо в консоли. Для линукс-систем есть более расширенная справка, которую можно вызвать через команду:

```
>man curl
```

Кроме того, почитать о CURL можно тут:
* https://ru.wikipedia.org/wiki/CURL
* https://curl.se/docs/ (официальная документация)
