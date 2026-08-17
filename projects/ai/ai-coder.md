# AI Coder

## Суть

Локальный/облачный AI-агент для помощи в кодировании: сбор контекста, генерация изменений, применение патчей (Streamlit UI).

## Стек

- Python, Streamlit
- Pydantic schemas
- Google Gemini + local LLM (LM Studio-compatible)
- Orchestrator / applicator / context packer

## Highlights

- Оркестрация шагов генерации и применения правок
- Упаковка контекста репозитория под лимиты модели
- Отдельные планы/ТЗ версий (v1–v8)

## Где код

Репозиторий `ai-dev-toolkit` → `AI_Coder/` (отдельный private/public репозиторий по необходимости).
