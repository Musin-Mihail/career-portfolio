# Техническая характеристика инструментария (Project Toolkit Specification)

В данном репозитории представлен набор инструментов собственной разработки (Self-hosted Tools), предназначенных для автоматизации разработки, обработки данных, CI/CD процессов и подготовки контекста для AI.

### 1. Автоматизация и кодогенерация (Automation & Code Generation)

Инструменты для ускорения разработки микросервисной архитектуры и устранения бойлерплейта.

- **Full Stack Code Generator (`generate_full_stack.py`):**
- **Функционал:** Автоматическая генерация слоев Backend (C# .NET) и Frontend (Angular) на основе декларативных словарей.
- **Backend генерация:** Создает контроллеры, модели данных и сниппеты для `DbContext` (EF Core), реализуя паттерн Repository/Service.
- **Frontend генерация:** Создает сервисы API, конфигурации таблиц, маршруты (Routes) и формы редактирования для Angular.
- **Особенности:** Преобразование именования (PascalCase -> kebab-case), работа с файловой системой.
- **OpenAPI Client Generator (`generate_api_typescript.ps1`):**
- **Функционал:** PowerShell-скрипт для автоматического скачивания Swagger/OpenAPI спецификаций с микросервисов и генерации TypeScript-клиентов для Angular.
- **Технологии:** PowerShell, `openapi-generator-cli`.

### 2. Подготовка контекста для LLM/AI (AI Context Extraction)

Продвинутые скрипты для сбора кодовой базы в единый контекст, что позволяет эффективно использовать LLM (ChatGPT/Claude) для рефакторинга и анализа больших проектов.

- **Smart Code Extractor (`extractor.js`):**
- **Функционал:** Рекурсивный обход проекта (Node.js) с построением графа зависимостей.
- **Логика:** Использует `dependency-cruiser` для анализа импортов. Автоматически подтягивает связанные HTML шаблоны и SCSS стили для каждого TypeScript компонента.
- **Результат:** Генерирует единый файл с кодом и структурой проекта, отфильтровывая шум (node_modules, coverage).
- **Git Analytics & Change Dumper (`Git_stat`):**
- **Функционал:** Python-скрипты для анализа истории Git-репозитория.
- **Возможности:** Выгрузка статистики коммитов по сотрудникам, извлечение состояния файлов "До/После" изменений для ретроспективного анализа кода нейросетями.

### 3. GIS и Обработка данных (GIS Data Engineering & ETL)

Скрипты для миграции геоданных и трансформации административных границ.

- **GeoJSON Processor (`convert_regions.py`):**
- **Функционал:** ETL-скрипт для конвертации GeoJSON (границы стран/районов) в SQL-дампы для PostGIS.
- **Технологии:** Python, библиотеки `shapely` (работа с геометрией), `json`, `csv`.
- **Ключевые алгоритмы:**
- Исправление топологии (превращение "дырок" в полигонах в отдельные объекты).
- Маппинг координат на кастомную сетку (Mozaik Grid System).
- Генерация SQL `INSERT` стейтментов с поддержкой транзакций.
- Локализация названий (RU/EN/AR) через JSON-словари.

### 4. Web Scraping и сбор данных

Инструменты для агрегации данных из открытых источников.

- **Python Scrapers (`hh-scraper`, `factories`):**
- **Технологии:** `requests`, `BeautifulSoup` (bs4), работа с сессиями и Cookies.
- **Функционал:** Парсинг каталогов предприятий и вакансий, обход пагинации, защита от блокировок (User-Agent ротация, задержки), экспорт в CSV.
- **Chrome Extension (`my-data-saver`):**
- **Технологии:** Manifest V3, JavaScript.
- **Функционал:** Браузерное расширение для точечного извлечения данных со сложных SPA-сайтов (HeadHunter) прямо из DOM-дерева активной вкладки.
- **Traffic Analyzer (`YandexMap/process_har.py`):**
- **Функционал:** Анализ HAR-архивов (сетевого трафика браузера) для извлечения скрытых данных JSON API, которые невозможно получить прямым парсингом HTML.

### 5. DevOps и Инфраструктура

Конфигурация среды развертывания.

- **Docker Orchestration (`docker-compose.yml`):**
- **Стек:** Настройка связки .NET Core Monolith, PostgreSQL, Minio (S3 storage), GeoServer и Nginx.
- **Особенности:** Настройка Healthchecks, Volumes, сетей и переменных окружения для разных режимов (Development/Production).
- **Database Migrations (`apply_all_migrations.bat`):**
- **Функционал:** Автоматизация наката SQL-миграций на несколько баз данных PostgreSQL с обработкой кодировок (BOM/UTF-8) и конфигурируемым списком задач.

---

### Ключевые навыки, подтвержденные этим кодом (Skills Matrix)

| Категория           | Технологии и навыки                                                                 |
| ------------------- | ----------------------------------------------------------------------------------- |
| **Languages**       | Python (Advanced), JavaScript/Node.js, C#, PowerShell, Batch                        |
| **Data Processing** | ETL pipelines, JSON/CSV manipulation, Regex, AST parsing                            |
| **GIS / Geo**       | PostGIS, GeoJSON, Shapely, Geometry validation, Coordinate systems                  |
| **Web / Network**   | Web Scraping (BS4, Selenium concepts), REST API, HTTP Headers/Cookies, HAR analysis |
| **DevOps**          | Docker, Docker Compose, CI/CD scripting, Postgres Administration (`psql`)           |
| **Architecture**    | Code Generation, Dependency Injection knowledge (Angular/.NET), Microservices setup |

### Резюме для портфолио (Summary)

> "Разработал экосистему утилит для повышения продуктивности команды ("Developer Experience"). Набор включает в себя автоматизированные генераторы Full Stack кода (.NET + Angular), сложные ETL-пайплайны для обработки GIS-данных (GeoJSON -> PostGIS) и инструменты статического анализа зависимостей для подготовки технической документации и контекста для AI. Опыт создания кастомных парсеров (Python/Chrome Extensions) и настройки контейнеризированных сред (Docker Compose)."
