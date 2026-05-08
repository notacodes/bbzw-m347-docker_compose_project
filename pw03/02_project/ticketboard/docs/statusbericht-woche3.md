# Statusbericht – Woche 3

## Umgesetzte Arbeiten
- `.env` erstellt mit DB-Zugangsdaten
- `.gitignore` und `.dockerignore` erstellt
- `compose.yml`: Hardcodierte Werte durch `${VARIABLE}` ersetzt
- `main.py`: DATABASE_URL via `os.getenv()` aus `.env` gelesen

## Aktueller Stand
System startet mit `docker compose up --build`. `/health` und `/db-check` funktionieren.

## Probleme
Keine.