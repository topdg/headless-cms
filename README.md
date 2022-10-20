# Headless CMS
## Базово
Как устроен мир
* Системы состоят из 2-х частей
  1. То, что мы видим - визуальная - называется **Front-end**.
  2. То, что скрыто от нас - данные, хралища данных, все, что связано с обработкой **на сервере** - **Back-end**
    Front-end явялется визуализацией данных, полученных с Back-end, грамотный подход - разделение этих данных, когда Back-end не зависим от Front-end.
* Как наши сайты работают сейчас:
  1. Пользователь открывает страницу
  2. В этот момент происходит обращение к базам данных
  3. Базы данных обрабатывают запрос пользователя
  4. Мы обрабатываем, полученные из баз данных данные (да-да, тавтология)
  5. Генерируем пользователю конечный результат

## Для продвинутых пользователей
Мы в данный момент используем подход, который при каждом заходе пользователя загружает, обрабатывает данные, которые по-факту являются одинаковыми и неизменяемыми. 100 пользователей в день, заходящие на одну и ту же страницу 100 раз увидят одно и тоже содержание, но выполнят тысячи обращений к Back-end, чтобы получить один и тот же результат, тем самым излишне напрягая сервер. Что в принципе снижает его пропускую способность.

Умы этого мира подумали и поняли, что делать так не имеет смысла, а можно один раз обратиться к серверу (Back-end), получить данные, обработать их, сгенерировать итоговую страницу и всем пользователям показывать эту заранее сгенерированную страницу, обходя пункты (2-5). То есть получается схема, при которой:
1. Пользователь открывает страницу
2. Мы возвращаем готовую страницу

Реализовав подобный подход, умы пошли дальше, они поняли, что мы поскольку единожды генерируем статичную страницу, можно генерировать ее максимально облегченной для пользователя, добавив автогенерацию картинок, сжатие всего и вся. Что существенно облегчило загрузку страниц для конечного пользователя.

Но и на этом умы не остановились, поскольку теперь Front-End отделен от Back-end, нам не обязательно держать админку по общедоступному и известному всем адресу, когда у нас есть сайт.ru , а админка располагается по сайт.ru/wp-admin/ . Теперь наша админка может быть где угодно, на любом другом домене или поддомене. Тем самым мы гарантируем безопастность нашему сервису, что хакеры или другие автоматизированные программы не будут совершать попыток взлома, потому что они просто не имеют прямого доступа к серверу, они даже не знают, где он расположен.

Но и на этом преимущества не заканчиваются, т.к. Back-end отделен от Front-end. Front-end может быть любым, то есть, мы можем отображать наши данные, которые хранятся где-то на сервере на любых устройствах. Грубо говоря, если заказчик через время захочет сделать себе приложение на телефон, он автоматически получает место, откуда может эти данные получать, условно приложение клиники может быть связано с админкой на WordPress ровно, так же как и основной сайт.

Тогда умы задумались еще сильнее, в результате чего появились так называемые PWA (прогрессивные веб-приложения). Это механизм, который позволяет скачать сайт на телефон в виде приложения, в реальности это обычный сайт, просто работает как приложение. Хороший пример, когда Сбер попал под санкции и был заблокирован в магазинах приложений, они на своем сайте сделали возможность сказачать PWA, тем самым дав пользователям пользоваться Сбербанк Online почти так же удобно, как и в обычном приложении.

## Так что такое фреймворки
Front-end, как правило, создается на *JavaScript фреймворках* (самые популярные React, Vue, Angular, Svelte). Фрейморк очень удобен в использовании и разработке. Они изначально придуманы для работы над большими проектами (React, например, придумали разработчики Facebook) и используется сейчас он повсеместно во всем мире. Особенно это полезно именно большим сайтам, корпорациям.

Когда придумывали эти фреймворки, не сильно думали на счет обычных статичных сайтов, потому что мир программистов так устроен, что тут дают механизмы, а ты должен уметь ими управлять в своих интересах. Поэтому итогом разработки сайта на фреймворке получается приложение, которое не будет индексироваться роботом, потому что они работают по принципу, как мы сейчас (5 этапов), только они отображают страницу за счет JavaScript, тем самым поисковые роботы просто не видят контента страницы. 

Тогда другие большие умы подумали, что это не самая удобная реализация в моментах, когда нужны статичные сайты, которые будут хорошо индексироваться, и придумали механизмы-библиотеки, которые взаимодействуя с фреймворком, генерируют как раз статичные сайты, как было описано выше. Одина из таких библиотек *Gatsby*, которую я и предлагаю в качестве дальнейшего инструмента разработки.

## Что такое Headless CMS
В обычном мире существовали CMS - системы управления сайтом, самой популярной из которых мы пользуемся - *WordPress*. А так же существуют и любые другие админки, которые так же позволяют редактировать/изменять контент страницы/портала. Так вот, фреймворки по-факту, используются для создания как-нибудь подобных админок, потому что там много логических-динамических вещей, которые удобно реализовать. Условно, наступит день, когда админку WordPress напишут на фреймворке, ибо этот процесс и так уже частично происходит.

В нашем мире писать свою админку на каждый проект - абсурдно, поэтому мы и используем WordPress. Он дает базовые вещи, которые и помогают создавать сайт и удобно его редактировать из админ-панели. Поэтому нам не стоит отказываться от готовых CMS систем.

Headless CMS - это когда есть CMS - она служит, как админка, но существует отдельно, только для того, чтобы мы могли редактировать/добавлять/удалять данные на сайт. Соответственно, мы из этой админки берем данные и генерируем станицы сайта. Поэтому я и настаиваю последнее время, чтобы мы все потихоньку уносили в админку, это и удобно редактировать, и задел на будущее. Потому что в последствии мы сможем сохранив наши админки, использовать их в качестве Headless CMS.

И тут мир дает нам уникальную возможность объединить нашу админку WordPress и какой-нибудь фреймворк, благодаря API, который предоставляет WordPress. То есть, мы можем взять готовую админку от WordPress - это будет наш Back-end, сделать сайт на фреймворке React с использованием Gatsby. Благодаря чему наши сайты станут быстрыми и безопастными.

## Итог, как это будет работать
Создается админка, можно сделать что-то типо macmiror.topdg.ru (тут будет админка макмирора или admin.macmiror.ru, короче что угодно), есть сайт macmiror.ru. Переделав сайт macmiror.ru на React+Gatsby, мы получим множество статически сгенерированных HTML-страничек, которые и будут показаны на сайте macmiror.ru. Таким образом мы получаем преимущества в безопастности, потому что никто не знает, что наша админка находится на macmiror.topdg.ru, а так же потому, что статичный сайт практически невозможно взломать (исключая взлом сервера). Прирост производительности, за счет снижения нагрузки на сервер, а также прирост скорости загрузки страниц за счет внутренних оптимизаций обеспеченных комбинацией React+Gatsby.