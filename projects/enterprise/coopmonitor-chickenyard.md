# CoopMonitor (ChickenYard) — Smart Poultry Farm Management

## Суть

**CoopMonitor** — edge-система мониторинга и управления птицеводческими комплексами. Объединяет IoT-телеметрию микроклимата, производственный учёт (падеж, корм, вода, болезни), видеонаблюдение с AI-аналитикой и автоматическую отчётность.

Репозиторий кода: отдельный git (`ChickenYard`), не входит в это портфолио. Работодатель — [6th Grain](../../experience/6th-grain.md). Доведён до Release Candidate одним инженером, затем handover команде сопровождения. Продукт по **12-Factor App**, без хардкода секретов/портов, **multi-tenancy** (изолированные инстансы ферм через `INSTANCE_NAME` и динамические `PORT_*`).

## Роль

Full-stack / system design: архитектура, .NET API, Angular UI, Python AI-сервис, Docker-инфраструктура, безопасность и наблюдаемость.

## Стек

| Слой          | Технологии                                                           |
| ------------- | -------------------------------------------------------------------- |
| Frontend      | Angular 21, PrimeNG (Aura), TailwindCSS, HLS.js, ngx-translate       |
| Backend       | C# / .NET 10, EF Core, SQLite (WAL), Quartz.NET, Serilog, Mapster    |
| AI            | Python 3.12, FastAPI, PyTorch, Ultralytics (YOLO/RTDETR), OpenCV     |
| Infra         | Docker Compose, Nginx (API Gateway), MinIO (S3), MediaMTX (RTSP→HLS) |
| Observability | Grafana + Loki + Promtail (PLG)                                      |
| QA            | xUnit, Playwright E2E                                                |

## Архитектура

```text
Browser → Nginx (SPA + /api + /api-ai + /hls)
            ├─ .NET 10 API  ↔  MinIO
            ├─ Python AI    ↔  MinIO  (analyze → webhook)
            └─ MediaMTX (HLS/RTSP)
```

- **API Gateway:** фронтенд-контейнер раздаёт статику и проксирует трафик — без CORS-проблем и прямого проброса внутренних портов.
- **AI pipeline:** fire-and-forget + webhooks; очередь задач защищает от OOM при пиковой нагрузке.
- **Security:** JWT + RBAC; fail-fast в Production без сложного пароля/JWT; секреты только из `.env`; межсервисный API key.
- **Алерты:** Telegram + Email при критических отклонениях.
- **Отчёты:** фоновая генерация HTML/PDF (Quartz + PuppeteerSharp).

## Ключевые возможности

- Дашборды микроклимата (T, H, CO₂, NH₃), расход корма/воды, FCR и производственные KPI
- Видеостена HLS и AI-детекция аномалий (паника/падеж/аудио-паттерны)
- Журналы учёта с фото/видео-доказательствами в MinIO
- Аудит действий и ролевая модель доступа
- Изоляция инстансов для разных ферм на одном хосте

## Highlights для резюме

- Спроектировал и довёл до production-ready RC end-to-end IoT/AI-систему: .NET 10 + Angular Signals + Python CV
- Выстроил Docker-инфраструктуру медиа: MinIO + MediaMTX + Nginx gateway + PLG-логирование
- Реализовал асинхронный AI-пайплайн (S3 → inference → webhook) и матрицу алертов
- Закрыл zero-hardcode / multi-tenant конфигурирование для on-prem развёртывания
