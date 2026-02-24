# M300 – WordPress als Web-Dienstleistung

## 1. Dienstleistungskonzept

### Zweck der Dienstleistung

Diese Dienstleistung stellt eine containerisierte Webhosting-Lösung für kleine Unternehmen bereit.
Ziel ist es, eine einfach wartbare, portable und isolierte Umgebung für eine Firmenwebsite bereitzustellen.

### Warum diese Lösung?

 Viele KMU benötigen:

eine kostengünstige Website

einfache Wartung

Datensicherheit

schnelle Wiederherstellung bei Fehlern

Durch Docker kann die gesamte Umgebung reproduzierbar bereitgestellt werden.


### Inbetriebnahme

Container starten:
```bash
docker compose up -d
```
Status prüfen:
```bash
docker ps
```
### Zugriff / Ports

WordPress: http://localhost:8081 (Port 8081 → Container-Port 80)

cAdvisor: http://localhost:8080 (Monitoring)

### Volumes

Die Daten werden persistent gespeichert über Named Volumes:

db_data (Speichert db Dateien)

wp_data (Speichert wordpress Dateien)