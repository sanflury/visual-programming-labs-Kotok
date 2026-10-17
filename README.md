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

### lab3/ — Bubble

- `docs/`
  - `api.md` — документация API Connector (JSONPlaceholder)
  - `report.md` — отчёт по лабораторной работе №3
- `screenshots/` — скриншоты всех шагов
  - `01-prompt.png`, `01-prompt-footer.png` — Часть 1 (генерация)
  - `02.1-buildguide.png` … `02.4-buildguide.png` — Часть 2 (Build Guides)
  - `03.1-title.png`, `03.2-global-variable.png`, `03.3-style.png`, `03.4-component.png` — Часть 3 (UI)
  - `04.1-data-type.png`, `04.1-data-records.png` — Часть 4.1 (Data Type)
  - `08-appointments-page.png`, `08-workflow-create.png`, `08-workflow-delete-confirm.png`, `09-workflow-create-result.png`, `09-workflow-delete-result.png`, `10-workflow-update-form.png`, `10-workflow-update-result.png` — Часть 4.2 (CRUD)
  - `11-api-*.png` — Часть 5 (Ачивка 1: API Connector)

**Ачивка 1. API Connector** — подключён публичный тестовый API **JSONPlaceholder** (GET, POST, PUT, DELETE), результат отображается на странице `api-demo`.

### lab4/ — n8n

- `docs/`
  - `redis.md` — документация по работе с Redis
  - `report.md` — отчёт по лабораторной работе №4
- `flows/` — экспортированные workflow n8n
  - `01-manual-set.json` — Manual Trigger → Set → Code
  - `02-code.json` — Manual Trigger → Code → NoOp
  - `03-if.json` — Manual Trigger → Code → IF → 2× NoOp
  - `04-set.json` — Manual Trigger → Set (timestamp) → Code
  - `05-http.json` — Manual Trigger → HTTP Request → Code
  - `06-schedule.json` — Schedule Trigger → Code
  - `09-redis-set.json` — Redis Set → Get
  - `10-redis-delete.json` — Redis Delete → Get
  - `11-ollama.json` — Ollama (Ачивка 1.1)
- `screenshots/` — скриншоты всех workflow
- `n8n-data/` — данные n8n (в `.gitignore`)
- `n8n-files/` — рабочая папка `/data` (в `.gitignore`)

**Ачивка 1.1. Ollama** — подключена локальная LLM (Qwen 2.5-0.5B) через Ollama, использована в workflow `11-ollama`.

## Ачивки

- **lab2. Ачивка 4** — Swagger / OpenAPI документация: реализована вручную через HTML-страницу `api-docs.html`, доступную по `/docs`.
- **lab3. Ачивка 1** — API Connector: подключён JSONPlaceholder, 4 эндпоинта (GET, POST, PUT, DELETE), документация в `lab3/docs/api.md`.
- **lab4. Ачивка 1.1** — Ollama: подключена локальная LLM, использована в workflow `11-ollama`.