# Отчёт по лабораторной работе №2. Node-RED

**Студент:** Коток Александра · **Группа:** УИР-241

## Краткое описание

В ходе работы я освоила Node-RED как low-code инструмент. Настроила
Node-RED в Docker с volume, собрала **13 потоков**, покрывающих базовые
и расширенные ноды, реализовала 3 GET-эндпоинта, dashboard с графиком
и gauge, Telegram-бота, работу с файлами и с контекстом. Также взяла
**ачивку №4** (Swagger/OpenAPI документация).

## Какие AI-промпты использовались

- «Сгенерируй код для function node на JavaScript: принять число, создать массив, применить цикл for, вернуть объект с полем payload»
- «Как настроить MQTT-брокер `broker.hivemq.com` в Node-RED для публикации и подписки на один топик?»
- «Как подключить `node-red-dashboard` и настроить gauge и chart?»
- «Сгенерируй Mustache-шаблон для вывода полей объекта в текстовый вид»

## Какие ноды освоены

| Раздел | Ноды |
|---|---|
| Общие | inject, debug, complete, catch, status |
| Функции | function, switch, change, range, template |
| Сеть | http in, http response, http request, mqtt in, mqtt out |
| Хранилище | write file, read file |
| Dashboard | gauge, chart |
| Telegram | receiver, sender |
| Анализ | json |

## Способ установки, версии

- **Способ:** Docker Desktop, образ `nodered/node-red`
- **Команда запуска:**
  ```
  docker run -d -p 1880:1880 -v <local>:/data --name mynodered nodered/node-red
  ```
- **Версия Node-RED:** 5.0.7
- **Версия Node.js:** 24.20.0

## Потоки и скриншоты

Все скриншоты — в папке `screenshots/`:

| Поток | Файл flow | Скриншот |
|---|---|---|
| 2.1 Inject → Debug | `flow-01-inject-debug.json` | `01-inject-debug.png` |
| 2.2 Function node | `flow-02-function.json` | `02-function.png` |
| 2.3 Switch node | `flow-03-switch.json` | `03-switch.png` |
| 2.4 Change node | `flow-04-change.json` | `04-change.png` |
| 2.5 Template node | `flow-05-template.json` | `05-template.png` |
| 2.6 HTTP Request | `flow-06-http-request.json` | `06-http-request.png` |
| 2.7 MQTT | `flow-07-mqtt.json` | `07-mqtt.png` |
| 2.8 GET-эндпоинты | `flow-08-endpoints.json` | `08-endpoints-*.png` (6 шт.) |
| 2.9 Dashboard | `flow-09-dashboard.json` | `09-dashboard-nodes.png`, `09-dashboard-ui.png` |
| 2.10 Telegram-бот | `flow-10-telegram.json` | `10-telegram-nodes.png`, `10-telegram-chat.png` |
| 2.11 Файлы | `flow-11-files.json` | `11-files-nodes.png`, `11-files-record.png` |
| 2.12 Контекст | `flow-12-context.json` | `12-context.png` |
| Ачивка 4 | `flow-13-swagger-docs.json` | `13-swagger-*.png` |

## Выводы

Node-RED оказался удобным инструментом для быстрого прототипирования
IoT- и API-решений. Большинство задач решается перетаскиванием нод,
а код нужен только в function. Особенно полезными оказались MQTT,
Dashboard и работа с файлами. Поняла, как работает flow context для
хранения состояния между сообщениями и как настроить Telegram-бота
через BotFather.

Из минусов — автоматические генераторы Swagger в Docker-образе
Node-RED устанавливаются проблемно (конфликт зависимостей), поэтому
документацию пришлось сделать вручную в виде HTML-страницы.

## Ачивка 4. Swagger / OpenAPI

Автоматический модуль `node-red-contrib-scalar-docs` **не установился**
в Docker-образе Node-RED (конфликт зависимостей). Вместо него я
реализовала документацию **вручную** — HTML-файл `api-docs.html`
со списком всех эндпоинтов, описанием параметров и ответов, а также
**кликабельными ссылками** для тестирования каждого эндпоинта.

Страница отдаётся через эндпоинт `/docs` цепочкой:
```
http in (GET /docs) → read file (/data/api-docs.html) → http response
```

**Доступ:** `http://localhost:1880/docs`

Это полноценный UI с работающими запросами — все три эндпоинта можно
протестировать прямо со страницы.