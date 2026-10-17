# Отчёт по лабораторной работе №4. n8n

**Студент:** Коток Александра · **Группа:** УИР-241

## Краткое описание выполненного

В ходе работы я освоила **n8n** как low-code платформу автоматизации. Установила n8n в Docker, изучила базовые и продвинутые ноды, настроила **Redis** и реализовала создание/удаление ключа. Выполнила **Ачивку 1.1** — подключила локальную LLM через **Ollama** и использовала её в workflow.

### Установка n8n

- **Способ:** Docker Desktop, образ `n8nio/n8n`.
- **Команда запуска:**
  ```bash
  docker run -d --name n8n -p 5678:5678 \
    -v C:\...\lab4\n8n-data:/home/node/.n8n \
    -v C:\...\lab4\n8n-files:/data \
    -e N8N_SECURE_COOKIE=false \
    --restart unless-stopped n8nio/n8n
  ```
- **Версия n8n:** `2.43.7` (см. Settings → About).
- **Два volume:** один для `.n8n` (данные), второй для `/data` (файлы).

## Какие AI-промпты использовались

- «Как установить n8n в Docker с volume для данных и файлов?»
- «Синтаксис Code node в n8n: как получить данные из предыдущей ноды и вернуть объект?»
- «Как настроить HTTP Request в n8n для получения JSON с публичного API?»
- «Как подключить Ollama к n8n через Docker (host.docker.internal)?»
- «Какая модель Ollama самая маленькая для быстрого теста?»

## Освоенные ноды

### Триггеры
- **Manual Trigger** — ручной запуск.
- **Schedule Trigger** — запуск по расписанию.

### Обработка данных
- **Edit Fields (Set)** — изменение полей.
- **Code** — выполнение JavaScript.
- **If** — ветвление.
- **No Operation** — пустышка (для завершения веток).

### Сеть
- **HTTP Request** — запросы к API.

### Хранилище
- **Redis (Set)** — запись ключа.
- **Redis (Get)** — чтение ключа.
- **Redis (Delete)** — удаление ключа.

### AI
- **Basic LLM Chain** — цепочка с LLM.
- **Ollama Chat Model** — локальная модель через Ollama.

## Скриншоты

Все скриншоты — в папке `screenshots/`:

- `01-version.png` — версия n8n (2.43.7).
- `02-manual-set.png` — flow-01: Manual → Set → Code.
- `03-code.png` — flow-02: Manual → Code → NoOp.
- `04-if.png` — flow-03: Manual → Code → IF → 2× NoOp.
- `05-set.png` — flow-04: Manual → Set → Code.
- `06-http.png` — flow-05: Manual → HTTP Request → Code.
- `07-schedule.png` — flow-06: Schedule → Code.
- `08-redis-set.png` — flow-09: Redis Set → Get.
- `09-redis-delete.png` — flow-10: Redis Delete → Get.
- `11-ollama.png` — flow-11: Ollama (Ачивка 1.1).

## Часть 2. Workflows

### 2.1. Manual Trigger → Set → Code (`flow-01`)

- **Manual Trigger** — ручной запуск.
- **Set**: `payload = "Коток"`, `topic = "lab4/kotok/basic"`.
- **Code**: выводит данные в консоль, возвращает объект.

### 2.2. Code node (`flow-02`)

- Использован **JavaScript**: `const`, `let`, массив, цикл `for`, `if/else`, объект.
- Результат: объект `{user, status, doubled, count}`.

### 2.3. IF node (`flow-03`)

- **Code** формирует `payload`.
- **IF** проверяет `payload == "большое"`.
- **True** → NoOp, **False** → NoOp.

### 2.4. Set node с timestamp (`flow-04`)

- **Set**: `topic`, `timestamp` = `{{ $now.toISO() }}`, `payload`.
- **Code**: выводит complete msg object.

### 2.5. HTTP Request (`flow-05`)

- **HTTP Request**: `GET https://catfact.ninja/fact`.
- **Code**: выводит ответ API.

### 2.6. Schedule Trigger (`flow-06`)

- **Schedule Trigger**: каждую минуту.
- **Code**: возвращает текущее время.

## Часть 3. Redis

- **Redis** запущен в Docker на порту **6380** (6379 был занят другим контейнером).
- **Credentials** в n8n: `host.docker.internal:6380`, без пароля.
- **Workflow 09-redis-set**: Set → Get. Результат: `Тестовое значение из n8n`.
- **Workflow 10-redis-delete**: Delete → Get. Результат: `propertyName: null` (ключа нет).

Подробнее — в `docs/redis.md`.

## Часть 4. Ачивка 1.1 — Ollama

- **Ollama** установлена через `.exe` на Windows.
- **Модель**: `Qwen 2.5-0.5B` (скачана через зеркало ModelScope).
- **Credential** в n8n: `Base URL = http://host.docker.internal:11434`.
- **Workflow 11-ollama**: Manual Trigger → Basic LLM Chain → Ollama Chat Model.
- **Промпт**: «Расскажи интересный факт про кошек».
- **Результат**: модель ответила текстом про кошек.

## Выводы

В ходе работы я освоила **n8n** как low-code платформу: установку в Docker, базовые и продвинутые ноды (Set, Code, IF, HTTP Request, Schedule), работу с **Redis** (создание, чтение, удаление ключей). Отдельно разобралась с **локальными LLM** через **Ollama**: скачала модель, подключила к n8n и использовала в workflow.

Главный практический вывод: **n8n** — мощный инструмент для автоматизации. Он сложнее Node-RED, но даёт **больше контроля** и **готовые ноды** для AI, Redis, HTTP. **Ollama** позволяет запускать **локальные модели бесплатно**, без интернета и API-ключей — это удобно для прототипирования и тестов.

## Ачивка 1.1 — объяснение для защиты

«Я установила Ollama через официальный установщик для Windows. Скачала модель Qwen 2.5-0.5B через зеркало ModelScope. В n8n создала credential с Base URL `http://host.docker.internal:11434` — это позволяет контейнеру n8n обращаться к Ollama, которая работает на хосте. Собрала workflow: Manual Trigger → Basic LLM Chain → Ollama Chat Model. В промпте написала "Расскажи интересный факт про кошек" — модель ответила текстом. Это доказывает, что локальная LLM подключена и работает.»