# Содержание документа

[Описание проекта и задачи](https://github.com/AlexanderBeli/robots_factory?tab=readme-ov-file#r4c---robots-for-consumers)

[Реализация задач](https://github.com/AlexanderBeli/robots_factory?tab=readme-ov-file#выполнение-заданий)

# R4C - Robots for consumers

## Небольшая предыстория.
Давным-давно, в далёкой-далёкой галактике, была компания производящая различных 
роботов. 

Каждый робот(**Robot**) имел определенную модель выраженную двух-символьной 
последовательностью(например R2). Одновременно с этим, модель имела различные 
версии(например D2). Напоминает популярный телефон различных моделей(11,12,13...) и его версии
(X,XS,Pro...). Вне компании роботов чаще всего называли по серийному номеру, объединяя модель и версию(например R2-D2).

Также у компании были покупатели(**Customer**) которые периодически заказывали того или иного робота. 

Когда роботов не было в наличии - заказы покупателей(**Order**) попадали в список ожидания.

---
## Что делает данный код?
Это заготовка для сервиса, который ведет учет произведенных роботов,а также 
выполняет некие операции связанные с этим процессом.

Сервис нацелен на удовлетворение потребностей трёх категорий пользователей:
- Технические специалисты компании. Они будут присылать информацию
- Менеджмент компании. Они будут запрашивать информацию
- Клиенты. Им будут отправляться информация
___

## Как с этим работать?
- Создать для этого проекта репозиторий на GitHub
- Открыть данный проект в редакторе/среде разработки которую вы используете
- Ознакомиться с задачами в файле tasks.md
- Написать понятный и поддерживаемый код для каждой задачи 
- Сделать по 1 отдельному PR с решением для каждой задачи
- Прислать ссылку на своё решение

# Выполнение заданий

## Реализован API-endpoint, принимающий и обрабатывающий информацию в формате JSON. 
В результате web-запроса на этот endpoint, в базе данных появляется запись 
отражающая информацию о произведенном на заводе роботе.

Реализована валидация входных данных, на соответствие существующим в системе моделям.

Протестировано с помощью библиотеки httpie ручным тестированием через cli.

Пример запроса:

```http POST http://127.0.0.1:8000/robots/api/v1/ {"model":"R2","version":"D2","created":"2024-12-14 23:59:59"}```

Пример ответа:

```HTTP/1.1 200 OK
Content-Length: 85
Content-Type: application/json
Cross-Origin-Opener-Policy: same-origin
Date: Tue, 17 Dec 2024 16:37:16 GMT
Referrer-Policy: same-origin
Server: WSGIServer/0.2 CPython/3.13.0
X-Content-Type-Options: nosniff
X-Frame-Options: DENY

{
    "created": "2024-12-14 23:59:59",
    "model": "R2",
    "serial": "R2-D2",
    "version": "D2"
}
```

Добавил db.sqlite3 в демонстрационных целях

## Реализована возможность скачать по прямой ссылке Excel-файл со сводкой по суммарным показателям производства роботов за последнюю неделю.

Файл включает в себя несколько страниц, на каждой из которых представлена информация об одной модели, но с детализацией по версии.

Данная функция доступна по адресу:

```http://127.0.0.1:8000/download-excel/```

Пример файла доступен в папке summary_example

## Реализована отправка уведомлений заказчику по факту появления товара на складе

Посмотреть код можно [здесь](https://github.com/AlexanderBeli/robots_factory/blob/main/orders/signals.py).