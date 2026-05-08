# Fragen – Integration der Services (DL10)

Name: <Nachname> <Vorname>
Klasse: <Klasse>

---

## 1. Services verstehen

Welche Services haben Sie in Ihrer `compose.yaml` definiert?

Antwort: api, db, adminer, frontend

---

Welche Aufgabe hat jeder Service in Ihrem System?

Antwort:
- api: Stellt die REST-API (FastAPI) für das TicketBoard bereit
- db: PostgreSQL-Datenbank zur persistenten Speicherung der Tickets
- adminer: Webinterface zur Administration und Verwaltung der Datenbank
- frontend: nginx-Webserver, der die statische HTML-Oberfläche ausliefert

---

## 2. Service-Kommunikation

Welchen Servicenamen verwendet die API, um die Datenbank zu erreichen?

Antwort: db

---

Warum funktioniert `localhost` innerhalb eines Containers nicht für die Kommunikation mit anderen Services?

Antwort: localhost zeigt innerhalb eines Containers nur auf den Container selbst, nicht auf andere Container. Jeder Container hat seine eigene Netzwerk-Umgebung.

---

Wie stellt Docker Compose sicher, dass sich Services gegenseitig finden können?

Antwort: Docker Compose erstellt ein eigenes DNS-Netzwerk. Alle Services sind über ihren Servicenamen aus der compose.yaml erreichbar.

---

## 3. Ports und Zugriff

Über welche Ports sind folgende Services erreichbar?

- API: 8000
- Adminer: 8080
- Frontend: 3000

Antwort: API auf 8000, Adminer auf 8080, Frontend auf 3000 (jeweils Host-Port)

---

Welcher Unterschied besteht zwischen:

- Container-Port
- Host-Port

Antwort: Der Container-Port ist der Port innerhalb des Containers (z. B. 80 bei nginx). Der Host-Port ist der Port auf dem lokalen Rechner, der auf den Container-Port weiterleitet (z. B. 3000:80). Nur der Host-Port ist von ausserhalb des Docker-Netzwerks erreichbar.

---

## 4. Persistenz

Was passiert mit den Daten, wenn ein Container ohne Volume gelöscht wird?

Antwort: Alle Daten im Container-Dateisystem gehen verloren, da sie nur temporär存在于 der beschreibbaren Schicht des Containers waren.

---

Wie haben Sie die Persistenz für die Datenbank umgesetzt?

Antwort: Mit einem named Volume `postgres_data`, das im db-Service unter `/var/lib/postgresql/data` eingebunden ist.

---

Warum ist ein Volume für die Datenbank notwendig?

Antwort: Damit die Datenbankdaten auch nach einem `docker compose down` oder Container-Neustart erhalten bleiben. Ohne Volume wären alle Daten beim Löschen des Containers verloren.

---

## 5. Compose-Konfiguration

Welche Elemente haben Sie in Ihrer `compose.yaml` definiert?

Antwort: services (api, db, adminer, frontend), volumes (postgres_data), sowie build, image, ports, environment, env_file, depends_on und volumes-Mounts pro Service.

---

Welche Umgebungsvariablen sind für die Datenbank-Verbindung notwendig?

Antwort: POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD (für die initiale DB-Konfiguration). Die Verbindungsdaten werden aus der .env-Datei geladen.

---

Wofür wird `depends_on` verwendet?

Antwort: `depends_on` legt die Startreihenfolge der Container fest. Der api-Container startet erst, nachdem der db-Container gestartet wurde. Es wartet jedoch nicht auf die vollständige Verfügbarkeit der Datenbank.

---

## 6. Systemtest

Hat das System beim ersten Start vollständig funktioniert?

Antwort: Ja, alle Services starten und sind erreichbar. Die Datenbankverbindung kann konfiguriert werden.

---

Welche Probleme sind aufgetreten?

Antwort: Keine nennenswerten Probleme, da die Dockerfiles bereits vollständig und funktionsfähig waren.

---

Wie haben Sie diese Probleme gelöst?

Antwort: -

---

## 7. Verständnis

Beschreiben Sie kurz den Datenfluss in Ihrem System.

Antwort: Browser → Frontend (nginx, Port 3000) → API (FastAPI, Port 8000) → DB (PostgreSQL, Port 5432). Adminer greift direkt auf die DB zu.

---

Was passiert beim Befehl:

```bash
docker compose down
```

Antwort: Alle Container werden gestoppt und entfernt. Das definierte Volume `postgres_data` bleibt erhalten. Das Standard-Netzwerk wird ebenfalls entfernt.

---

## 8. Reflexion

Was war für Sie heute die wichtigste Erkenntnis?

Antwort: -

---

Was war schwierig oder noch unklar?

Antwort: -
