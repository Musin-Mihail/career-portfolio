# Competitive advantages

Формулировки только из [`../experience/`](../experience/README.md) и [`../projects/`](../projects/_index.md). Lead здесь — **product/tech ownership**, не управление людьми. Платформу PortalPA / Agroportal **не разрабатывал**. Английский — B1.

Полный разбор для работодателя. Короткая версия — в [`../README.md`](../README.md).

## 1. Продукт целиком одним инженером до RC и handover

Не «закрыл тикеты в команде», а полный цикл: требования, архитектура, код, Docker, тесты, документация, передача сопровождению.

- **VineTrack** — единственный инженер MVP vine-to-bottle ([карточка](../projects/enterprise/vinetrack.md)).
- **CoopMonitor / ChickenYard** — IoT/AI-мониторинг птицефермы до Release Candidate, затем handover команде сопровождения ([карточка](../projects/enterprise/coopmonitor-chickenyard.md)).

Исходники обоих продуктов **не публичные**. Доказательства глубины — описания и стек в карточках проектов.

## 2. Встраивание модуля в чужую платформу без ownership платформы

Для VineTrack: dual auth (`Standalone` / `Integrated`), schema ownership, FK только по UUID, ADR и handover со стороны модуля. Код ЛК PortalPA не писал. Это граница, которую на рынке middle/senior редко формулируют явно.

## 3. AgriTech full-stack, не слайды

PostGIS, Sentinel-2 / GDAL, MapLibre Dual-View, Dexie offline, IoT + MediaMTX, computer vision (YOLO/RTDETR) в рабочем контуре — не обёртка над чат-ботом. GIS-цикл 6th Grain (ноябрь 2025 — март 2026) и два последующих R&D-продукта это подтверждают.

## 4. AI-Augmented Engineering как процесс

Кодогенерация (`generate_full_stack`) и context packers. Дисциплина поставки с LLM, а не лозунг «умею ChatGPT».

## 5. Железо и пользовательский продукт

- **HikrobotScanner** — WPF / .NET 9, промышленные камеры по TCP/IP ([карточка](../projects/desktop/hikrobot-scanner.md), [код](https://github.com/Musin-Mihail/Tool_Hikrobot_Scanner)).
- **The Numbers** — выпущенная игра на Yandex Games ([карточка](../projects/gamedev/the-numbers.md), [код](https://github.com/Musin-Mihail/Game_The_numbers), [стора](https://yandex.ru/games/app/451308)).

Код доходит до конвейера и до стора, не только до PR.

## 6. Операционный формат

Удалёнка из Филиппин, гражданство РФ, готовность к командировкам. Разрешения на работу (из снимка hh.ru): Великобритания, Германия, Испания, Италия, Канада, Китай, Нидерланды, Россия. Это логистика найма, не биография.

## Ограничения (не раздувать)

| Тема | Как есть |
|------|----------|
| Грейд Lead | Ownership продукта и архитектуры. Не team lead с подчинёнными. |
| Английский | B1: technical reading; интервью на английском — зона роста. |
| PortalPA | Внешняя платформа. Только контракты интеграции со стороны VineTrack. |
| Публичный код | VineTrack и ChickenYard закрыты. Смотреть пины: [`../projects/github-inventory.md`](../projects/github-inventory.md). |
