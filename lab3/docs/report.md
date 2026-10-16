# Отчёт по лабораторной работе №3. Bubble

**Студент:** Коток Александра · **Группа:** УИР-241

## Часть 1. Промпт

Дословно промпт, который был отправлен в AI-агент Bubble:

```
Создай приложение на тему «Список врачей клиники»
Пусть этот сайт будет публичный (без регистрации)
Страницу обязательно создай по структуре header + body + footer
Обязательно укажи в заготовке следующую строку: «ТВП: Коток»
Добавь несколько интерактивных элементов (реализующих CRUD):
список врачей в виде карточек, форму добавления нового врача,
кнопки редактирования и удаления для каждой карточки
```

## Что сгенерировал AI

Приложение «Список врачей клиники» с:

- **Header** с логотипом и кнопкой «Добавить врача».
- **Body** с сеткой карточек (20 врачей), фильтром по специализации.
- **Footer** с контактами клиники и строкой `ТВП: Коток`.
- **CRUD-элементами:** добавление, редактирование, удаление.

### Скриншоты

- `screenshots/01-prompt.png` — главная страница приложения
- `screenshots/01-prompt-footer.png` — футер со строкой `ТВП: Коток`

## Часть 2. Build Guides

Изучила гайд из каталога **Build Guides** (про поиск и обновление
элементов с одинаковым стилем).

**Что показалось полезным:**

- Инструмент **App search tool** — поиск всех элементов одного типа
  на странице.
- Принцип централизованного обновления множества элементов
  через один стиль.

**Что взяла в своё приложение:**

- Применила **App search tool**, чтобы найти все кнопки «Удалить»
  в приложении.

**Скриншоты:**

- `screenshots/02.1-buildguide.png` — список гайдов.
- `screenshots/02.2-buildguide.png` — открытый гайд.
- `screenshots/02.3-buildguide.png` — все кнопки на странице.
- `screenshots/02.4-buildguide.png` — найдены кнопки «Удалить».

## Часть 3. Ручная доработка UI

### 3.1. Изменён текст заголовка

Добавила своё имя к заголовку: «Список врачей — Коток Александра».

Скриншот: `screenshots/03.1-title.png`

### 3.2. Создана Global variable для цвета

Через **Styles → Variables → Colors** создала переменную `primary-color`
со значением синего цвета. Применила к кнопке «Добавить врача».

Скриншот: `screenshots/03.2-global-variable.png`

### 3.3. Создан новый стиль

Через **Styles → New Style** создала стиль `Primary Label` для текста.
Стиль использует переменную `primary-color` для цвета текста.
Применила стиль к подписи «СПРАВОЧНИК КЛИНИКИ».

Скриншот: `screenshots/03.3-style.png`

### 3.4. Привнесён готовый компонент

Из библиотеки **Components** (раздел **Marketing**) перетащила блок **Feature section**.
Настроила под свою тему: переписала на русский, добавила описания
преимуществ клиники, подобрала картинки медицинской тематики.

Скриншот: `screenshots/03.4-component.png`

## Часть 4. Data и Workflows

### 4.1. Создание сущности Appointment

**AI-промпт для сущности:**

```
Придумай сущность для приложения "Список врачей клиники".
Нужно название сущности и минимум 4 поля разных типов:
текст, дата, да/нет, число.
Поля должны описывать запись на приём к врачу.
```

**Ответ AI:** сущность `Appointment` (Приём) с полями:

| Поле | Тип | Описание |
|---|---|---|
| `patientName` | text | ФИО пациента |
| `doctorName` | text | ФИО врача |
| `appointmentDate` | date | дата и время приёма |
| `cabinetNumber` | number | номер кабинета |
| `price` | number | стоимость приёма |
| `isCompleted` | yes/no | состоялся ли приём |
| `documentUrl` | text | ссылка на заключение |

**Что сделано:**

- Создан Data Type `Appointment` в **Data → Data types**.
- Добавлены 7 полей разных типов (text, date, number, yes/no).
- Добавлены 3 записи вручную через **App Data**.

**Скриншоты:**

- `screenshots/04.1-data-type.png` — поля сущности Appointment.
- `screenshots/04.1-data-records.png` — 3 записи в App Data.

### 4.2. Workflows CRUD

Реализован полный CRUD для сущности `Appointment` через workflows
на странице `appointments`:

**Create (создание):**
- Кнопка «Добавить приём» открывает модальную форму.
- Форма содержит поля: patientName, doctorName, appointmentDate,
  price, cabinetNumber, isCompleted.
- По кнопке «Сохранить» создаётся новая запись Appointment.

**Read (чтение):**
- Список приёмов отображается через Repeating Group.
- Каждая карточка показывает данные из базы.

**Update (обновление):**
- Кнопка «Редактировать» открывает форму с заполненными данными.
- При изменении и сохранении запись обновляется в базе.

**Delete (удаление):**
- Кнопка «Удалить» показывает диалог подтверждения.
- После подтверждения запись удаляется из базы.

**Скриншоты:**
- `screenshots/08-appointments-page.png` — страница приёмов (Read).
- `screenshots/08-workflow-create.png` — форма создания (Create).
- `screenshots/09-workflow-create-result.png` — результат создания.
- `screenshots/10-workflow-update-form.png` — форма редактирования (Update).
- `screenshots/11-workflow-update-result.png` — результат изменения.
- `screenshots/08-workflow-delete-confirm.png` — подтверждение удаления (Delete).
- `screenshots/09-workflow-delete-result.png` — результат удаления.

## Часть 5. Ачивка 1. API Connector

### Подключённый API

Использовала публичный тестовый API **jsonplaceholder.typicode.com** — не требует регистрации и токенов.

### Настроенные эндпоинты

В **API Connector** создана коллекция с 4 вызовами:

| Метод | Название | URL |
|---|---|---|
| GET | Get Post | `jsonplaceholder.typicode.com/posts/1` |
| POST | Create Post | `jsonplaceholder.typicode.com/posts` |
| PUT | Update Post | `jsonplaceholder.typicode.com/posts/1` |
| DELETE | Delete Post | `jsonplaceholder.typicode.com/posts/1` |

**Use as:** `Data`, **Data type:** `JSON` — для всех вызовов.

### Отображение в UI

Создана страница **`api-demo`** с 4 кнопками. Каждая кнопка запускает свой workflow:

1. Вызов API (Get/Create/Update/Delete Post).
2. `Delete a list of ApiResponses` — очистка предыдущих результатов.
3. `Create a new ApiResponse` — сохранение результата (title, body, id).

Результат показывается в **Repeating Group** под кнопками через **`Current cell's ApiResponse's title`**.

**Тип данных `ApiResponse`:** поля `title` (text), `body` (text), `id` (number).

### Скриншоты

- `screenshots/11-api-datatype-1.png` — Data Type `ApiResponse`.
- `screenshots/11-api-datatype-2.png` — поля Data Type.
- `screenshots/11-api-get.png` — GET с ответом.
- `screenshots/11-api-post.png` — POST с `id: 101`.
- `screenshots/11-api-put.png` — PUT с обновлённым заголовком.
- `screenshots/11-api-delete.png` — DELETE (empty object).
- `screenshots/11-api-page-1.png` — Preview после «Создать пост».
- `screenshots/11-api-page-2.png` — Preview после «Получить пост».
- `screenshots/11-api-page-3.png` — Preview после «Обновить пост».
- `screenshots/11-api-page-4.png` — Preview после «Удалить пост».
- `screenshots/11-api-workflow.png` — workflow одной из кнопок.

### Объяснение для защиты

«Подключила публичный API **jsonplaceholder** через встроенный **API Connector** Bubble. Настроила 4 эндпоинта: GET, POST, PUT, DELETE. Для каждого создала кнопку на странице `api-demo`. Результат каждого вызова сохраняется в **Data Type `ApiResponse`** и отображается в **Repeating Group**. Перед сохранением нового результата старые записи удаляются — список показывает **только последний результат**. DELETE возвращает пустой объект — для него создаётся запись со статичным текстом «Пост удален», чтобы визуально показать результат. jsonplaceholder — тестовый API, он **не сохраняет изменения** между вызовами, но **все 4 метода успешно работают** — это видно по ответам в API Connector.»

## Ссылки

- **Dev-версия приложения:** `https://my-app-261014-18320.bubbleapps.io/version-test/api-demo`

## Выводы

В ходе работы я освоила **Bubble** как no-code платформу: генерацию приложения через AI-агента, ручную доработку UI, работу с **Global variables** и **стилями**, проектирование **базы данных** и настройку **workflows для CRUD**.

Отдельно разобралась с **API Connector**: подключила внешний API, настроила 4 вызова (GET, POST, PUT, DELETE), реализовала **сохранение и отображение результата** на странице.

Главный практический вывод: **AI-агент сильно ускоряет** создание каркаса приложения, но **финальную логику и UI нужно проверять и дорабатывать вручную** — особенно в части условий видимости, работы с данными и API.