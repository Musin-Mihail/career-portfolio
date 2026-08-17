# Technical profile

Детальный стек и проекты. Работодатели и даты — только в [`../experience/`](../experience/README.md). Не добавлять опыт, которого нет в `experience/` и `projects/`.

## 1. Professional Identity

**Lead R&D / Senior Full-Stack Engineer (.NET + Angular) & AI Integrator.**  
Сейчас — единственный инженер **VineTrack** (6th Grain). Системное мышление: microservices / modular monolith, Enterprise .NET, Angular Signals, прикладной AI (local LLM, RAG, multi-agent, CV). DX: собственные кодогенераторы и context packers.

Конкурентные преимущества и ограничения роли: [`competitive-advantages.md`](competitive-advantages.md). Публичный код: [`../projects/github-inventory.md`](../projects/github-inventory.md).

---

## 2. Technical Stack (Skill Matrix)

| Domain                   | Key Technologies & Tools                                                                                                                                                               |
| ------------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Backend (.NET)**       | **C# (.NET 6/8/9/10 Preview)**, ASP.NET Core Web API, Entity Framework Core, **RabbitMQ** (Messaging), **SignalR** (Real-time), Quartz.NET (Scheduling), Serilog.                      |
| **Backend (Python)**     | **Python 3.10+**, **FastAPI** (Async), SQLAlchemy, Pydantic v2, Aiosqlite, BeautifulSoup4, Selenium.                                                                                   |
| **Frontend**             | **Angular 16+** (Standalone, **Signals**, RxJS), TypeScript, Angular Material, SCSS, Tailwind, Vite.                                                                                   |
| **AI & ML Engineering**  | **Local LLMs** (`llama-cpp-python`, GGUF), **RAG** (ChromaDB, `sentence-transformers`), **Multi-Agent Systems**, Prompt Engineering (Chain-of-Thought, YAML config), Google GenAI SDK. |
| **Desktop / Industrial** | **WPF (MVVM)**, CommunityToolkit.Mvvm, Hardware Integration (Hikrobot Scanners via TCP/IP), Printing/Barcode generation (ZXing.Net).                                                   |
| **GameDev**              | **Unity (C#)**, ECS concepts, Addressables, Yandex Games SDK, Mobile IAP (Unity IAP), WebGL Optimization.                                                                              |
| **DevOps & Tools**       | **Docker**, Docker Compose, Nginx, Linux (Ubuntu), PowerShell Scripting, CI/CD concepts, **PostgreSQL**, SQLite.                                                                       |

---

## 3. Key Architectural Patterns & Concepts

В каждом проекте я применяю строгие архитектурные стандарты:

- **Clean Architecture / Onion:** Четкое разделение на API, Domain, Application и Infrastructure слои (проекты _Interactive Portfolio, Role-Play, VineTrack_).
- **Microservices & Event-Driven:** Использование RabbitMQ для асинхронного общения между сервисами (проект _Interactive Portfolio_).
- **MVVM (Model-View-ViewModel):** Глубокое понимание паттерна как в Desktop (WPF), так и в Web (Angular Services) (проекты _HikrobotScanner, Crossword_).
- **Service Locator & DI:** Реализация собственных DI контейнеров в Unity и использование стандартных в .NET/Angular.
- **Automated Code Generation:** Разработка собственных инструментов для генерации Boilerplate-кода (Full Stack Gen, OpenAPI clients) для ускорения разработки.

---

## 4. Project Showcase (Evidence of Skills)

### 🔹 Enterprise & Web Systems

**1. Interactive Portfolio (.NET 8 / Angular / RabbitMQ)**

- _Суть:_ Full-Stack система с микросервисными элементами.
- _Tech Highlight:_ Реализован паттерн **Fire-and-Forget** через RabbitMQ для тяжелых задач. Frontend на **Angular Signals** (Zone-less ready). Интеграция real-time уведомлений через **SignalR**.
- _Testing:_ Unit (xUnit, Vitest) и E2E (Cypress) тесты.

**2. CoopMonitor / ChickenYard (.NET 10 / Angular / AI Vision)**

- _Суть:_ Edge-система мониторинга птицефермы: IoT-телеметрия, HLS-видео, AI vision/audio, отчёты и алерты.
- _Tech Highlight:_ **.NET 10** + Angular 21 Signals, Python FastAPI (YOLO/RTDETR), Docker Compose (Nginx gateway, MinIO, MediaMTX, PLG), JWT/RBAC, multi-tenant on-prem, 12-Factor конфигурация.

**3. VineTrack (.NET 10 / Angular 21 / PostGIS)**

- _Суть:_ Вертикальный MVP-модуль для винодельческих хозяйств — цифровой двойник «от лозы до бокала» (GIS, агрономия/IPM, Smart Cellar, QR-прослеживаемость).
- _Tech Highlight:_ Clean Architecture + MediatR CQRS, PostgreSQL/PostGIS, dual auth (`Standalone` / PortalPA `Integrated`), MassTransit/MinIO/SignalR AI-контур, MapLibre Dual-View + Dexie offline. **PortalPA не разрабатывал** — только подготовил границы интеграции (schema ownership, ADR/handover).

**4. Developer Toolkit (Automation Scripts)**

- _Суть:_ Экосистема утилит для повышения продуктивности (DX).
- _Tech Highlight:_
- `generate_full_stack.py`: Генерирует слои Backend (C# Controller/Service) и Frontend (Angular Service/Component) по декларативному описанию.
- GIS-пайплайны: ETL процессы для конвертации GeoJSON -> PostGIS.

### 🔹 AI & LLM Integration

**5. Role-Play Engine (Python FastAPI / Angular / Local LLM)**

- _Суть:_ Платформа для ролевых игр с AI-мастером.
- _Tech Highlight:_ **Мульти-агентная архитектура** (оркестратор управляет агентами: Narrative Planner, NPC, World Builder). Реализован **RAG** (ChromaDB) для долговременной памяти персонажей. Потоковая передача текста (SSE) на клиент.
- _Architecture:_ Чистая архитектура на Python (Separation of Concerns).

**6. English Tutor AI (Python / Google GenAI)**

- _Суть:_ Образовательная платформа без классической БД.
- _Tech Highlight:_ **No-DB Architecture** (хранение данных в Markdown-файлах для человекочитаемости). Интеграция с Google Gemini API через прокси. Агентная валидация ответов ученика.

### 🔹 Desktop & Industrial (WPF)

**7. HikrobotScanner (.NET 9 / WPF)**

- _Суть:_ ПО для промышленной автоматизации на конвейере.
- _Tech Highlight:_ Взаимодействие с "железом" (промышленные камеры) по TCP/IP. Высокопроизводительный UI с анимацией ошибок. Алгоритмическая валидация QR/Barcode кодов.

**8. Crossword Generator (.NET 6 / WPF)**

- _Суть:_ Генератор кроссвордов.
- _Tech Highlight:_ Реализация алгоритма **Backtracking** (поиск с возвратом) для генерации сетки. Сложный UI рендеринг через `Canvas` и `ItemsControl`.

### 🔹 Game Development (Unity)

**9. "The Numbers" & "Bobbles" (Unity / C#)**

- _Суть:_ Логические игры для WebGL (Yandex Games).
- _Tech Highlight:_ Оптимизация памяти (бинарная сериализация сетки для облачных сохранений). Событийно-ориентированная архитектура (ScriptableObject Events). Интеграция рекламы и покупок (IAP).

---

## 5. Education & Languages

- **Languages:** Russian (Native), English (B1).
- **Education:** см. [`education-languages.md`](education-languages.md)

---

> **Note for Recruiters:** I am not just a coder; I am a solution architect who builds tools to build software faster. I bridge the gap between complex backend logic, reactive frontends, and modern AI capabilities. Hiring narrative: [`competitive-advantages.md`](competitive-advantages.md).
