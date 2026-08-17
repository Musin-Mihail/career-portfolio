# 6th Grain Corporation

Сайт: [6grain.com](https://www.6grain.com/)  
Период: ноябрь 2025 — настоящее время  
Формат: удалённо

Два последовательных грейда в одной компании. Продукты AgriTech / IoT: GIS-платформа точного земледелия, edge-мониторинг птицефермы (CoopMonitor / ChickenYard), вертикальный модуль виноградарства (**VineTrack**).

**Граница роли:** код платформенного ЛК (PortalPA / Agroportal) **не разрабатывал**. Для VineTrack — dual auth, schema ownership, ADR и handover со стороны модуля.

Не публиковать: внутренние URL, секреты, appsettings, имена прод-БД, клиентские данные.

---

## Lead R&D Engineer / AI-Augmented Tech Lead

**Март 2026 — настоящее время**

Формат: one-man army. Полный цикл R&D: требования, архитектура, реализация, инфраструктура, тесты, документация и передача сопровождению.

### VineTrack (текущий продукт)

Единственный автор MVP «от лозы до бокала»: GIS виноградника, агрономия/IPM, урожай, Smart Cellar, QR-прослеживаемость.

- Clean Architecture .NET 10, MediatR CQRS, PostgreSQL / PostGIS, Angular 21 (Signals, MapLibre Dual-View, Dexie offline)
- Dual-mode auth/tenancy и границы схемы для встраивания в внешний ЛК
- Async-контур AI/снимков (MassTransit, MinIO, Quartz, SignalR) + публичный QR-паспорт (SSR)
- Docker-стек, CI, handover-документы; боевые ML-модели и мобильное приложение — зоны других команд (контракты API)

Карточка: [`../projects/enterprise/vinetrack.md`](../projects/enterprise/vinetrack.md)

### CoopMonitor / ChickenYard (Release Candidate, handover)

IoT/AI-мониторинг птицефермы, спроектированный и доведённый до RC одним инженером.

- Экосистема .NET 10 + Angular 21 + Python/FastAPI (CV)
- Медиа: MinIO + MediaMTX (RTSP→HLS), алерты, PLG (Promtail / Loki / Grafana)
- Clean Architecture + NetArchTest; Playwright E2E; документация C4 / API / domain для онбординга команды сопровождения

Карточка: [`../projects/enterprise/coopmonitor-chickenyard.md`](../projects/enterprise/coopmonitor-chickenyard.md)

---

## Full-Stack Engineer (.NET + Angular)

**Ноябрь 2025 — март 2026**

Развитие энтерпрайз-экосистемы точного земледелия (AgriTech, GIS).

- Геоанализ данных БПЛА: PostGIS (NetTopologySuite), GDAL, привязка ортофото и GeoTIFF к контурам полей
- Конвейер Sentinel-2: параллельная генерация индексов (NDVI, ARVI); bulk insert в PostgreSQL через Npgsql COPY
- CQRS (MediatR), батчирование EF Core, execution strategies
- Angular 17–21: config-driven UI (50+ справочников), карта (OSM/Leaflet), BBox-подгрузка (RxJS), Gantt на Signals/OnPush
- Интеграция модуля AI-прогноза урожайности в контур управления полями
