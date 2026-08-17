# VineTrack — Vine-to-Bottle Digital Twin (MVP)

## Суть

**VineTrack** — вертикальный модуль агро-платформы (Agroportal / PortalPA) для винодельческих хозяйств: цифровой двойник производства «от лозы до бокала». Объединяет GIS-микроменеджмент виноградника, агрономию и IPM, логистику урожая, Smart Cellar, лаб. данные, ESG/прослеживаемость и публичный QR-паспорт партии.

Репозиторий кода: отдельный git (`VineTrack`), не входит в это портфолио. Core API + Angular management UI + Python AI-stub в одном репо; мобильное offline-приложение и боевые ML-модели — зоны других команд (контракты API/webhook).

**Роль:** единственный инженер продукта (one-man army): архитектура, backend, frontend, Docker, интеграционные ADR. Работодатель — [6th Grain](../../experience/6th-grain.md), грейд Lead R&D (март 2026 — н.в.). Стек: Clean Architecture .NET 10 API, Angular 21 SPA, PostGIS, async AI-пайплайн, Docker, границы интеграции с PortalPA.

**Граница:** **PortalPA / Agroportal не разрабатывал** — только dual auth, schema ownership, domain bridges и handover со стороны модуля.

## Стек

| Слой             | Технологии                                                                  |
| ---------------- | --------------------------------------------------------------------------- |
| Backend          | .NET 10 / C#, MediatR CQRS, FluentValidation, EF Core, Gridify, MassTransit |
| Frontend         | Angular 21, Signals, NgRx SignalStore, PrimeNG, Tailwind, SSR, PWA          |
| GIS / Maps       | PostgreSQL 16 + PostGIS 3.4, NetTopologySuite, MapLibre GL, Turf.js         |
| Async / Realtime | RabbitMQ + MassTransit, Quartz.NET, SignalR, Redis                          |
| Storage / Docs   | MinIO (S3), QuestPDF, ClosedXML, QR                                         |
| AI node          | Python FastAPI stub (RabbitMQ consumer, S3, rasterio / Sentinel helpers)    |
| Infra / Ops      | Docker Compose, Traefik, Seq, OpenTelemetry, Serilog, GitHub Actions        |
| Offline          | Dexie (IndexedDB) sync + UI конфликтов                                      |
| i18n             | ngx-translate (ru / en / ar)                                                |

## Архитектура

```text
Browser / Traefik
  ├─ Angular SPA (management UI, MapLibre Dual-View, Dexie offline)
  ├─ Angular SSR public QR passport
  └─ .NET 10 API (MediatR vertical slices)
        ├─ PostgreSQL / PostGIS
        ├─ Redis / MinIO / RabbitMQ
        ├─ Quartz jobs + SignalR push
        └─ Python AI stub (webhook / queue)
```

- **Clean Architecture:** Domain → Application (Features/{Area}/Commands|Queries) → Infrastructure → thin Api host; контроллеры только через MediatR.
- **Dual auth:** `Standalone` (локальные Users + BCrypt + refresh) и `Integrated` (делегирование login в PortalPA, VineTrack JWT + `portal_access_token`).
- **Schema ownership:** PortalPA владеет `identity` / `core` / `reference`; VineTrack — схема `vinetrack` (или `public` в standalone); FK только по UUID; `ExcludePortalOwnedEntities` для shared DB.
- **Farm tenancy / RBAC:** заголовок `X-Farm-Id`, `FarmPermissionCodes`, object-level assignments (plot / row / trellis…).
- **API surface:** канон `/api/v1/{kebab}` + legacy aliases до cutover в ЛК; OpenAPI → typed Angular client.
- **Интеграционная подготовка (без разработки PortalPA):** ADR-001, DOMAIN-MAPPING, MODULES-MERGE, HANDOVER; bridge `Plot.PlatformFieldId`; меню/фасад auth под форму ЛК; inspection-schemes adapter.

## Ключевые возможности

- **GIS / цифровой двойник:** виноградники, сезоны, посадки, участки (GeoJSON/KML), ряды/шпалеры, Dual-View карта↔таблица, паспорт участка (PDF)
- **Агрономия:** задачи / журнал / канбан, калькуляторы (формулы JSON), удобрения и баковые смеси, фенология
- **IPM / почва / мониторинг:** пробы почвы, ловушки, скаутинг, аномалии, IoT-телеметрия
- **AI / remote sensing (stub + контракты):** фото → AI webhook, Ground Truth routing, Sentinel / Data Fusion jobs
- **Урожай и Smart Cellar:** партии, танки / ферментация, граф прослеживаемости, SSCC-хелперы, лаб. тесты
- **Traceability / ESG UX:** публичный QR-паспорт партии, жалобы/аналитика, ECO-сигналы
- **Ops:** отчёты и подписчики, weekly agro PDF/Excel, экспорт CSV под 1C/ERP, sync conflicts UI, catalogs / i18n
- **DevEx:** полный Docker-стек, smoke/verify-скрипты, CI (dotnet test + Angular build)

## Highlights для резюме

- Спроектировал и реализовал MVP вертикального агро-модуля vine-to-bottle: .NET 10 CQRS + Angular 21 + PostGIS
- Выстроил dual-mode auth/tenancy и границы схемы для безопасной интеграции с внешней платформой PortalPA (без ownership платформенного кода)
- Собрал async-контур AI/спутников (MassTransit, MinIO, Quartz, SignalR) и публичный QR-паспорт с SSR
- Закрыл GIS Dual-View UI (MapLibre) и offline Dexie-синхронизацию с разбором конфликтов
- Подготовил ADR/handover и API-контракты для встраивания модуля в ЛК платформы

## Связанные материалы

- Опыт: [`../../experience/6th-grain.md`](../../experience/6th-grain.md)
- Код: отдельный репозиторий VineTrack (не публичный)
- Внешняя платформа (контекст интеграции, **не мой код**): PortalPA / Agroportal
