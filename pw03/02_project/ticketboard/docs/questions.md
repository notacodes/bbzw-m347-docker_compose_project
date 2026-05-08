# Fragen – Konfiguration und Umgebungsvariablen (DL11)

Name: <Nachname> <Vorname>
Klasse: <Klasse>

---

## 1. Konfiguration

Welche Werte waren ursprünglich hardcoded in `compose.yml` und `app/main.py`?

Antwort:
In compose.yml: POSTGRES_DB=ticketdb, POSTGRES_USER=ticketuser, POSTGRES_PASSWORD=secret, DATABASE_URL.
In main.py: DATABASE_URL = "postgresql://ticketuser:secret@db:5432/ticketdb"

---

Warum ist es ein Problem, Passwörter direkt in `compose.yml` einzutragen?

Antwort:
Weil compose.yml (bzw. compose.yaml) meist ins Git eingecheckt wird. Einmal committed bleibt das Passwort für immer im Git-Verlauf sichtbar.

---

Was ist der Unterschied zwischen `.env` und `.env.example`?

Antwort:
`.env` enthält echte Zugangsdaten und wird nicht ins Git eingecheckt.
`.env.example` ist eine Vorlage ohne echte Passwörter und wird ins Git eingecheckt.

---

Warum muss `.env` in `.gitignore` eingetragen sein?

Antwort:
Damit die sensiblen Daten nicht versehentlich ins Git-Repository committed werden.

---

## 2. Variablen in Compose

Wie referenziert man eine Variable aus `.env` in `compose.yml`?

Antwort:
Mit `${VARIABLE_NAME}` (z. B. `${POSTGRES_DB}`).

---

Was passiert, wenn eine Variable in `.env` fehlt, aber in `compose.yml` verwendet wird?

Antwort:
Docker Compose setzt einen leeren String ein oder gibt eine Warnung aus. Der Service kann dadurch fehlschlagen.

---

Was zeigt der Befehl `docker compose config`? Wann ist er nützlich?

Antwort:
Er zeigt die fertig aufgelöste Compose-Konfiguration mit allen ersetzten Variablen. Nützlich zum Prüfen, ob die Substitution korrekt funktioniert.

---

## 3. Dockerfile und Build

Warum wird `requirements.txt` in einem eigenen `COPY`-Schritt vor dem App-Code kopiert?

Antwort:
Damit Docker das Layer-Caching nutzen kann. Solange sich requirements.txt nicht ändert, wird der `pip install`-Schritt aus dem Cache verwendet.

---

Was bewirkt `.dockerignore`? Welche Dateien sollten darin stehen?

Antwort:
`.dockerignore` schliesst Dateien vom Docker-Build-Kontext aus. Es sollten `.env`, `.git`, `__pycache__`, `.venv` darin stehen.

---

## 4. Systemtest

Funktioniert `/db-check` nach Ihrer Konfigurationsanpassung?

Antwort:
Ja, `/db-check` gibt `{"db": "connected"}` zurück.

---

Was zeigt der Endpunkt `/db-check` an, wenn die Verbindung funktioniert?

Antwort:
`{"db": "connected"}`

---

## 5. Reflexion

Was war der wichtigste Schritt in dieser Woche?

Antwort:
Das Ersetzen der hardcodierten Werte durch `.env`-Variablen, damit keine Passwörter im Code stehen.

---

Was ist noch unklar oder möchten Sie besser verstehen?

Antwort:
Nichts
