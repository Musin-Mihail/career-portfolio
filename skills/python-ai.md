# Python & AI Engineering

## Уровень

Сильная прикладная интеграция LLM/агентов; Python как основной язык AI- и DX-инструментов.

## Стек

- Python 3.10+
- FastAPI (async), Flask, Streamlit
- Pydantic v2, SQLAlchemy, Aiosqlite
- BeautifulSoup4, Selenium (scraping)
- Google GenAI SDK, OpenAI-compatible clients → LM Studio
- Local LLMs: llama-cpp-python, GGUF
- RAG: ChromaDB, sentence-transformers
- Multi-agent orchestration, CoT / YAML prompt configs
- Computer Vision: OpenCV, Ultralytics YOLO (эксперименты)

## Где применялось

- VineTrack — FastAPI AI-stub (RabbitMQ/S3 webhook-контур для vision / Sentinel)
- Role-Play Engine — multi-agent + RAG + SSE
- English Tutor — Gemini, no-DB Markdown storage
- AI Coder — Streamlit-агент с apply patches
- Life OS — парсинг inbox → Gemini-отчёты
- generate_context / generate_full_stack — DX codegen
- MassVideoCreation, video_to_frames, vn_translator — media/LLM lab

## Практики

- Разделение orchestration / tools / schemas
- Человекочитаемое хранение (Markdown) где это продукт
- Промпт-инжиниринг как версионируемые артефакты
