# Przykład CLAUDE.md — Projekt Python

```markdown
# Serwis API w Pythonie

## Tech stack
- Python 3.12
- FastAPI
- SQLAlchemy 2.0 + Alembic (migracje)
- PostgreSQL
- Pydantic v2 (walidacja)
- Poetry (zarządzanie zależnościami)

## Struktura
- `app/` — główny moduł aplikacji
- `app/api/` — endpointy API (routery)
- `app/models/` — modele SQLAlchemy
- `app/schemas/` — schematy Pydantic
- `app/services/` — logika biznesowa
- `app/core/` — konfiguracja, security, database
- `alembic/` — migracje bazy danych
- `tests/` — testy (pytest)

## Konwencje
- PEP 8 + black formatter
- Type hints wszędzie
- Docstringi w Google style
- Async/await preferowane nad sync
- Testy: pytest + httpx.AsyncClient

## Uruchamianie
- `poetry run uvicorn app.main:app --reload` — dev
- `poetry run pytest` — testy
- `poetry run alembic upgrade head` — migracje

## Zasady
- Każdy endpoint ma Pydantic schema na wejściu i wyjściu
- Dependency injection przez FastAPI Depends
- Sekrety w .env (python-dotenv)
- Nie modyfikuj istniejących migracji Alembic
```
