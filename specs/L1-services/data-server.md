# L1 — Data-Server (Raspberry Pi Zero 2W)

> Status: Stub. Zu befüllen.

## Verantwortung

- Serial-Stream vom Arduino empfangen und parsen
- Messwerte in SQLite persistieren (timestamped)
- REST-API für Read-Zugriff bereitstellen (Latest, History, Stats)
- Auto-Reconnect bei Serial-Verbindungsverlust
- Steuerungsbefehle Richtung Arduino senden (geplant)

## Schnittstellen

| Schnittstelle | Richtung      | Vertrag                                   |
|---------------|---------------|-------------------------------------------|
| USB-Serial    | RX ← Arduino  | `contracts/serial-protocol.md`            |
| USB-Serial    | TX → Arduino  | TBD                                        |
| HTTP REST     | Server (5000) | `contracts/openapi/data-server.v1.yaml`   |

## Architektur-Eigenheiten

- **Multi-threaded**: Flask auf Main-Thread, Daemon-Thread liest Serial. Zugriff via `serial_lock`.
- **Staleness-Check**: HTTP 503 falls letzte Messung > 10 s alt.
- **SQLite**: Indizierte `timestamp`-Spalte für effiziente History-/Stats-Queries.

## Deployment

- Systemd-Unit `greenhouse-sensor.service`
- Deploy via `git pull` auf dem Pi
- Detail: siehe `~/Documents/greenhouse/docs/STATUS.md`

## TODO

- [ ] Endpoint zum Senden von Steuerungs-Befehlen an Arduino
- [ ] Auth (selbst für lokales Netz: zumindest API-Key?)
- [ ] Retention-Policy für SQLite (Pi hat begrenzten Speicher)
