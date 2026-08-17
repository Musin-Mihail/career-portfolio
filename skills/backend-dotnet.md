# Backend — .NET / C#

## Уровень

Senior: проектирование API, модульный монолит / микросервисы, EF Core, messaging, real-time.

## Стек

- **Язык/рантайм:** C#, .NET 6 / 8 / 9 / 10 Preview
- **Web:** ASP.NET Core Web API
- **ORM:** Entity Framework Core
- **Messaging:** RabbitMQ (асинхронные fire-and-forget задачи)
- **Real-time:** SignalR
- **Jobs:** Quartz.NET
- **Logging:** Serilog
- **БД:** PostgreSQL, PostGIS (GIS), SQLite где уместно

## Где применялось

- VineTrack — .NET 10 Clean Architecture, MediatR CQRS, EF Core + PostGIS, MassTransit, dual auth/tenancy
- CoopMonitor / ChickenYard — микросервисы, Docker, RBAC/аудит
- Interactive Portfolio — RabbitMQ + SignalR
- HikrobotScanner, Crossword — .NET desktop (см. desktop skills)

## Практики

- Чистое разделение слоёв (API / Domain / Application / Infrastructure)
- RBAC и аудит действий
- Интеграция с фронтендом через OpenAPI / typed clients
