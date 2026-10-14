# API Connector — JSONPlaceholder (Ачивка 1)

## Общие сведения

- **API:** JSONPlaceholder — бесплатный fake REST API для тестов и прототипов
  (из списка [public-apis](https://github.com/public-apis/public-apis), раздел Development).
- **Базовый URL:** `https://jsonplaceholder.typicode.com`
- **Авторизация:** не требуется.
- **Важно:** это «фейковый» API. Запросы POST/PUT/DELETE **принимаются**
  и возвращают корректный ответ, но **данные на сервере не сохраняются**
  (повторный GET `/posts/1` вернёт исходный пост). Поэтому результаты каждого
  вызова **сохраняются в базе самого Bubble-приложения** (тип данных `ApiResponses`).

## Настройка в Bubble

`Plugins → API Connector` → коллекция **`New Collection`**, 4 вызова.

Для всех:

- **Use as:** `Data`
- **Data type:** `JSON`
- Галочка **«Attempt to make the call from the browser»** — **снята**
  (вызов выполняется на стороне сервера).
- **Body type:** `JSON`.

---

## Эндпоинты

### 1. GET — Get Post

| Параметр | Значение |
|---|---|
| Метод и URL | `GET https://jsonplaceholder.typicode.com/posts/1` |
| Параметры | нет (id поста зашит в URL) |
| Тело запроса | нет |

**Ответ (200):**

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit\nsuscipit recusandae consequuntur expedita et cum\nreprehenderit molestiae ut ut quas totam\nnostrum rerum est autem sunt rem eveniet architecto"
}
```

---

### 2. POST — Create Post

| Параметр | Значение |
|---|---|
| Метод и URL | `POST https://jsonplaceholder.typicode.com/posts` |
| Параметры | нет |

**Тело запроса:**

```json
{
  "title": "Новый пост из Bubble",
  "body": "Тестовое содержимое",
  "userId": 1
}
```

**Ответ (201):** сервер возвращает те же поля и присваивает новый `id`:

```json
{
  "title": "Новый пост из Bubble",
  "body": "Тестовое содержимое",
  "userId": 1,
  "id": 101
}
```

---

### 3. PUT — Update Post

| Параметр | Значение |
|---|---|
| Метод и URL | `PUT https://jsonplaceholder.typicode.com/posts/1` |
| Параметры | нет (id поста в URL) |

**Тело запроса:**

```json
{
  "id": 1,
  "title": "Обновлённый заголовок",
  "body": "Обновлённый текст",
  "userId": 1
}
```

**Ответ (200):** эхо отправленного объекта:

```json
{
  "id": 1,
  "title": "Обновлённый заголовок",
  "body": "Обновлённый текст",
  "userId": 1
}
```

---

### 4. DELETE — Delete Post

| Параметр | Значение |
|---|---|
| Метод и URL | `DELETE https://jsonplaceholder.typicode.com/posts/1` |
| Параметры | нет |
| Тело запроса | нет |

**Ответ (200):** пустой объект `{}`
(Bubble показывает: **«The response of this call is an empty object»**).

---

## Как это работает в приложении

На странице **`api-demo`** — четыре кнопки:

- «Создать пост»
- «Получить пост»
- «Обновить пост»
- «Удалить пост»

Каждая кнопка запускает свой workflow (`Button … is clicked`).

**Пример — workflow кнопки «Удалить пост»:**

1. `New Collection - Delete Post` — вызов API (DELETE).
2. `Delete a list of ApiResponses` — очистка предыдущих результатов.
3. `Create a new ApiResponse` — запись результата (`id`, `title`, `body`) в базу.

Результат из `ApiResponses` отображается **текстом под кнопками**
(через Repeating Group с `Current cell's ApiResponse's title`).

**Тип данных `ApiResponses`:** поля `id` (число), `title` (текст), `body` (текст).

### Что сохраняется на каждую кнопку

| Кнопка | Что сохраняется в `ApiResponses` |
|---|---|
| Создать пост | `title` = «Новый пост из Bubble» |
| Получить пост | `title` = «sunt aut facere…» (пост №1) |
| Обновить пост | `id` = 1, `title` = «Обновлённый заголовок», `body` = «Обновлённый текст» |
| Удалить пост | `id` = 0, `title` = «Пост удален», `body` = «Удаление выполнено» |