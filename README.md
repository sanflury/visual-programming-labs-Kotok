# visual-programming-labs-kotok

Лабораторные работы по дисциплине «Технологии визуального программирования».

**Студент:** Коток Александра · **Группа:** УИР-241

## Структура

### lab1/ — Моделирование процессов с использованием Git и визуальных нотаций

- `docs/`
    - `process_description.md` — описание бизнес-процесса «Бронирование номера в отеле»
    - `sequence.md` — Sequence Diagram (Mermaid)
    - `flowchart.md` — Flowchart (Mermaid)
- `diagrams/`
    - `process.bpmn` + `process-bpmn.png` — BPMN-диаграмма
    - `activity.drawio` + `activity-uml.png` — UML Activity Diagram
- `report.md` — отчёт по лабораторной работе №1

### lab2/ — Node-RED

- `docs/`
    - `api.md` — документация GET-эндпоинтов
    - `report.md` — отчёт по лабораторной работе №2
- `flows/` — экспортированные потоки Node-RED
    - `flow-01-inject-debug.json` — Inject → Debug
    - `flow-02-function.json` — Function node
    - `flow-03-switch.json` — Switch node
    - `flow-04-change.json` — Change node
    - `flow-05-template.json` — Template node (Mustache)
    - `flow-06-http-request.json` — HTTP Request
    - `flow-07-mqtt.json` — MQTT (HiveMQ public broker)
    - `flow-08-endpoints.json` — 3 GET-эндпоинта
    - `flow-09-dashboard.json` — Dashboard (gauge + chart)
    - `flow-10-telegram.json` — Telegram-бот
    - `flow-11-files.json` — Чтение и запись файла
    - `flow-12-context.json` — Flow context (счётчик)
    - `flow-13-swagger-docs.json` — Ачивка 4: ручная Swagger/OpenAPI документация
- `screenshots/` — скриншоты всех потоков и UI
- `node-red-data/` — рабочие данные Node-RED (в `.gitignore`)

## Ачивки

- **Ачивка 4** — Swagger / OpenAPI документация: реализована вручную через HTML-страницу `api-docs.html`, доступную по `/docs`