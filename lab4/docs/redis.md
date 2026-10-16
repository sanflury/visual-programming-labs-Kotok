# Redis в n8n — создание и удаление ключа

## Установка Redis

**Redis запущен в Docker** на порту **6380** (порт 6379 занят другим контейнером `leadflowdev-redis-1`).

**Команда запуска:**

```bash
docker run -d --name redis-n8n -p 6380:6379 redis:7
```

**Проверка:**

```bash
docker ps
docker exec redis-n8n redis-cli ping
```

Второй командой должно вернуться `PONG`.

## Credentials в n8n

В **n8n → Personal → Credentials** создан новый credential **`Redis account`**:

| Параметр | Значение |
|---|---|
| Host | `host.docker.internal` |
| Port | `6380` |
| Password | *(пусто)* |
| Database Number | `0` |

**`host.docker.internal`** — это специальный хост Docker, через который контейнер n8n видит хост-машину (где запущен Redis).

Соединение проверено кнопкой **Test** → `Connection tested successfully`.

---

## Workflow 1 — `09-redis-set`

**Цепочка нод:**

```
Manual Trigger → Redis (Set) → Redis (Get) → Code
```

**Шаги:**

1. **Manual Trigger** — ручной запуск.
2. **Redis (Set)** — создаёт ключ:
    - **Key:** `kotok`
    - **Value:** `Тестовое значение из n8n`
    - **Expire:** выключено.
3. **Redis (Get)** — читает ключ `kotok` обратно.
4. **Code** — выводит результат в JSON.

**Результат Output:**

```json
{
  "key": "kotok",
  "value": "Тестовое значение из n8n"
}
```

**Скриншот:** `screenshots/08-redis-set.png`.

**Экспорт:** `flows/flow-09-redis-set.json`.

---

## Workflow 2 — `10-redis-delete`

**Цепочка нод:**

```
Manual Trigger → Redis (Delete) → Redis (Get) → Code
```

**Шаги:**

1. **Manual Trigger** — ручной запуск.
2. **Redis (Delete)** — удаляет ключ `kotok`.
3. **Redis (Get)** — пытается прочитать ключ `kotok`.
    - Если ключа **нет** — `propertyName: null`.
4. **Code** — проверяет, что ключа больше нет.

**Результат Output:**

```json
{
  "key": "kotok",
  "exists": false,
  "result": {
    "propertyName": null
  }
}
```

**`exists: false`** — значит, удаление сработало.

**Скриншоты:**
- `screenshots/09-redis-delete.png` — workflow.
- `screenshots/10-redis-delete-output.png` — Output в JSON.

**Экспорт:** `flows/flow-10-redis-delete.json`.

---

## Как это объяснить на защите

> «Redis — это хранилище типа ключ-значение в памяти. Я установила его в Docker на порту 6380 (6379 был занят другим контейнером). В n8n создала credential с хостом `host.docker.internal` и портом 6380.
>
> В первом workflow я записываю ключ `kotok` через ноду Redis Set, потом читаю его через Redis Get — значение совпадает.
>
> Во втором workflow я удаляю ключ через Redis Delete и проверяю через Redis Get — возвращается `propertyName: null`, то есть ключа действительно нет. В Code я это преобразую в `exists: false`.
>
> Итого: показал полный цикл работы с Redis — запись, чтение, удаление и проверку отсутствия.»