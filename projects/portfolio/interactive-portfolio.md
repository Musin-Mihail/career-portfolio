# Technical Specification: Interactive Portfolio Project

## 1. Обзор Системы (System Overview)

Проект представляет собой **Full-Stack веб-приложение**, демонстрирующее современные подходы к разработке.

- **Backend:** REST API на ASP.NET Core 8 с использованием PostgreSQL, Entity Framework Core и асинхронной очереди сообщений RabbitMQ.
- **Frontend:** SPA на Angular (Modern/Bleeding Edge версий) с использованием Standalone Components, Signals, SSR (Server-Side Rendering) и Vite.
- **Основная цель:** Демонстрация технических навыков (CRUD, Real-time communication, State Management, оптимизация производительности).
- **Код:** [Portfolio_Angular](https://github.com/Musin-Mihail/Portfolio_Angular) · [Portfolio_DotNet](https://github.com/Musin-Mihail/Portfolio_DotNet)
- **Live:** [angular-portfolio-pi-nine.vercel.app](https://angular-portfolio-pi-nine.vercel.app/)

---

## 2. Backend Architecture (.NET)

### 2.1 Стек технологий

- **Framework:** .NET 8 (ASP.NET Core Web API).
- **Database:** PostgreSQL (Driver: `Npgsql`).
- **ORM:** Entity Framework Core 8 (Code-First Migrations).
- **Message Broker:** RabbitMQ (`RabbitMQ.Client`).
- **Real-time:** SignalR.
- **Documentation:** Swagger / Swashbuckle.
- **Testing:** xUnit, Moq, Microsoft.AspNetCore.Mvc.Testing (Integration Tests), EF Core InMemory.

### 2.2 Ключевые компоненты и сервисы

- **`ProjectsController`**:
- Реализует CRUD операции для сущности `Project`.
- Поддерживает массовую загрузку (`/bulk`).
- Обрабатывает ошибки уникальности БД через `IDbErrorService`.

- **`NotificationController`**:
- Эндпоинт для демонстрации асинхронной обработки.
- Принимает сообщение -> отправляет в `RabbitMQProducer`.

- **`RabbitMQProducer`**:
- Сервис для публикации сообщений в очередь `notifications`.

- **`RabbitMQConsumer` (HostedService)**:
- Фоновая задача (`BackgroundService`).
- Слушает очередь `notifications`.
- При получении сообщения пересылает его всем подключенным клиентам через `NotificationHub` (SignalR).

- **`NotificationHub`**:
- SignalR хаб для broadcasting сообщений клиентам.

### 2.3 Модели данных (Database Schema)

**Table: `Projects**`

- `Id` (PK, int)
- `Title` (string, max 100, required)
- `Description` (text, required)
- `ImageUrl` (string, nullable)
- `ProjectUrl` (string, required)
- `Tags` (string array `text[]`)

### 2.4 Инфраструктура и Конфигурация

- **Docker:** Multi-stage build (Build -> Publish -> Runtime). Образ: `mcr.microsoft.com/dotnet/aspnet:8.0`.
- **CORS:** Настроен для разрешения запросов с `http://localhost:4200` и продакшн-домена Vercel.
- **Environment:** Разделение настроек через `appsettings.json` (Prod: PostgreSQL) и `appsettings.Development.json`.

---

## 3. Frontend Architecture (Angular)

### 3.1 Стек технологий

- **Framework:** Angular (версия ^20.x — экспериментальная/future build), Standalone API.
- **Build Tool:** Vite (via `@angular/build` & `@analogjs/vite-plugin-angular`).
- **State Management:** Angular Signals (`signal`, `computed`, `toSignal`), RxJS (для событийных потоков).
- **CSS Framework:** Tailwind CSS 3.4 + SCSS.
- **Testing:** Vitest (Unit), Cypress (E2E), Cypress-Axe (Accessibility).
- **SSR:** Angular Universal / Express server (`@angular/ssr`).

### 3.2 Архитектурные решения

- **Standalone Components:** Полный отказ от `NgModule`.
- **Lazy Loading:** Все основные маршруты (`/projects`, `/lab` и дочерние роуты лаборатории) загружаются лениво.
- **Reactivity:** Гибридный подход. `HttpClient` возвращает `Observable`, который преобразуется в сигнал через `toSignal` для использования в шаблонах.
- **SSR/Prerendering:** Настроена серверная гидратация (`provideClientHydration`) и Express сервер для API-проксирования.

### 3.3 "Лаборатория" (The Lab)

Раздел `/lab` служит песочницей для демонстрации Angular internals:

1. **Interceptor (`/lab/interceptor`):**

- Демонстрация перехвата HTTP запросов.
- Добавление заголовков (`X-Custom-Auth`).
- Централизованная обработка ошибок (404, 500, Client-side).

2. **NgZone Optimization (`/lab/ngzone`):**

- Сравнение обработки событий внутри и вне Angular Zone.
- Демонстрация `runOutsideAngular` для предотвращения лишних циклов Change Detection при `mousemove`.

3. **Directives (`/lab/directives`):**

- `*appUnless`: Структурная директива (инверсия `*ngIf`).
- `[appHighlight]`: Атрибутивная директива.

4. **Content Projection (`/lab/projection`):**

- Слоты контента с селекторами (`[card-title]`, `[card-body]`).

5. **Pipes (`/lab/pipes` & `/pipes-advanced`):**

- Демонстрация разницы между `pure: true` (мемоизация) и `pure: false` (пересчет при каждом CD).

6. **Backend Integration (`/lab/backend-test`):**

- Интеграция с реальным .NET API.

7. **RabbitMQ/SignalR (`/lab/rabbitmq`):**

- Демонстрация полного цикла: Angular -> API -> RabbitMQ -> Background Worker -> SignalR -> Angular.

### 3.4 UI Components (Shared)

- **`app-card`**: Универсальная карточка с проекцией контента.
- **`app-button`**: Кнопки с вариантами (`pulse`, `gradient`, `icon`) на базе Tailwind.
- **`app-toggle-switch` / `app-custom-checkbox**`: Кастомные форм-контролы (используют `model()` inputs).
- **`[appCard3d]`**: Директива для 3D-трансформации элемента при наведении мыши.
- **`[appParallax]`**: Директива для параллакс-эффекта через `IntersectionObserver`.

---

## 4. Схема потоков данных (Data Flow Maps)

### 4.1 Стандартный запрос данных (HTTP)

1. **Frontend (Angular):** Компонент `ProjectsComponent` инициализирует сигнал `state` через `toSignal`.
2. **Frontend:** `ProjectService` делает GET запрос.
3. **Frontend:** `ApiInterceptor` добавляет токен авторизации.
4. **Backend (.NET):** `ProjectsController` получает запрос.
5. **Backend:** EF Core извлекает данные из PostgreSQL.
6. **Backend:** Возвращает JSON.
7. **Frontend:** Сигнал обновляется, UI перерисовывается.

### 4.2 Real-time уведомления (Async Loop)

1. **Frontend:** Пользователь нажимает "Отправить сообщение" в `LabRabbitmqComponent`.
2. **Frontend:** POST запрос на `/api/Notification`.
3. **Backend:** `NotificationController` принимает сообщение.
4. **Backend:** `RabbitMQProducer` кладет сообщение в очередь `notifications`.
5. **Backend:** Контроллер сразу возвращает 200 OK (Fire-and-Forget).
6. **Backend (Background):** `RabbitMQConsumer` считывает сообщение.
7. **Backend:** `RabbitMQConsumer` вызывает метод `ReceiveMessage` на `NotificationHub`.
8. **Frontend:** `SignalRService` (слушающий сокет) получает ивент `ReceiveMessage`.
9. **Frontend:** Обновляет `Subject`, компонент показывает уведомление.

---

## 5. Тестирование и качество кода

### Backend (.NET)

- **Unit Tests:** xUnit + Moq. Тестирование сервисов (`NpgsqlErrorService`) и контроллеров.
- **Integration Tests:** `WebApplicationFactory`. Подмена БД на `InMemoryDatabase` и очередей на фейковые реализации для тестов API эндпоинтов.

### Frontend (Angular)

- **Unit Tests:** Vitest. Мокирование `HttpClient`, тестирование сигналов и DOM-взаимодействий.
- **E2E Tests:** Cypress.
- Сценарии навигации.
- Проверка фильтрации проектов.
- Проверка интерактивных элементов лаборатории (Drag & Drop, Hover эффекты).

- **Accessibility:** `cypress-axe` для автоматической проверки доступности (a11y).

---

## 6. Деплоймент (Deployment Context)

- **Frontend:** Vercel.
- Конфигурация `vercel.json`.
- Rewrites для API (`/api/(.*)` -> `/api/server.ts`).
- CSP заголовки (Content-Security-Policy).

- **Backend:** Railway (предположительно, на основе URL `dotnet-portfolio-production.up.railway.app`).
- PostgreSQL хостится там же.
- RabbitMQ доступен по AMQP.
