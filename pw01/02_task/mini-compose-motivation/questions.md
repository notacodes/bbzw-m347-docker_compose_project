# Fragen – Mini Compose Motivation

Name: <Nachname> <Vorname>  
Klasse: <Klasse>

---

## 1. Services verstehen

Welche Services sind in `compose.yaml` definiert?

Antwort:  
Die definierten Services sind `web`, `api` und `admin`.

---

Welcher Service verwendet ein fertiges Image (`image`)?

Antwort:  
Die Services `web` und `admin` verwenden das fertige Image `nginx:alpine`.

---

Welcher Service wird aus einem Dockerfile gebaut (`build`)?

Antwort:  
Der Service `api` wird aus einem Dockerfile gebaut.

---

## 2. Ports und Zugriff

Über welchen Host-Port ist der Web-Service **zu Beginn** erreichbar?

Antwort:  
Der Web-Service war zu Beginn über den Port `8080` erreichbar.

---

Welchen Port verwendet der API-Service?

Antwort:  
Der API-Service verwendet den Port `5000`.

---

Auf welchen Port haben Sie den Web-Service geändert?

Antwort:  
Der Web-Service wurde auf den Port `8000` geändert.

---

## 3. Verständnis Docker Compose

Warum ist Docker Compose in diesem Beispiel sinnvoll?

Antwort:  
Docker Compose ist sinnvoll, weil mehrere Services mit einem einzigen Befehl gestartet werden können und die gesamte Konfiguration in einer Datei übersichtlich beschrieben ist.

---

Was ist der Unterschied zwischen `image` und `build`?

Antwort:  
`image` verwendet ein fertiges Image (z. B. aus Docker Hub). `build` erstellt ein eigenes Image aus einem Dockerfile.

---

Was macht der Befehl `docker compose up --build`?

Antwort:  
Der Befehl baut alle Images mit `build` neu und startet anschliessend alle definierten Services.

---

## 4. Fehleranalyse

Startete das System beim ersten Versuch vollständig?

Antwort:  
Nein, das System startete beim ersten Versuch nicht vollständig.

---

Welcher Service hatte ein Problem?

Antwort:  
Der Service `api` hatte ein Problem.

---

Was war die Ursache für das Problem?

Antwort:  
Der Build-Kontext war falsch gesetzt (`build: .` statt `build: ./api`). Docker suchte das Dockerfile im falschen Verzeichnis.

---

Wie haben Sie das Problem gelöst?

Antwort:  
Der Build-Kontext wurde auf den richtigen Ordner angepasst (`build: ./api`).

---

## 5. Docker Compose CLI

Was ist der Unterschied zwischen:

- `docker compose stop`  
- `docker compose pause`  

Antwort:  
`stop` beendet den Container-Prozess vollständig. `pause` friert den Container ein (SIGSTOP), er bleibt im Speicher, führt aber keine Prozesse aus.

---

Was zeigt der Befehl `docker compose logs` an?

Antwort:  
Der Befehl zeigt die Konsolenausgaben (Logs) aller Container an, was bei der Fehlersuche hilft.

---

Was zeigt der Befehl `docker compose ps` an?

Antwort:  
Der Befehl zeigt den aktuellen Status der Container (ob sie laufen) und die verwendeten Ports.

---

## 6. Reflexion

Was war für Sie heute neu oder besonders wichtig?

Antwort:  
Wichtig war zu verstehen, wie der Build-Kontext funktioniert und dass ein falscher Pfad das gesamte System blockieren kann.

---

Was ist noch unklar oder möchten Sie noch besser verstehen?

Antwort:  
Wie Container untereinander kommunizieren und wie Daten mit Volumes dauerhaft gespeichert werden.
