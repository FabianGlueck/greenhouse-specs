# L0 — Systemarchitektur

> Status: Entwurf. Inhalt aus `CLAUDE.md` in `~/Documents/greenhouse/CLAUDE.md` zu migrieren.

## Vision

Smartes Balkon-Gewächshaus für Basilikum und Salat mit autonomer Bewässerung, Klimaregelung und Datenerfassung.

## Komponenten

```
Arduino Uno (Sensoren via I2C + analog)
    ↓ USB Serial @ 9600 baud  (siehe contracts/serial-protocol.md)
Raspberry Pi Zero 2W (Flask + SQLite)
    ↓ HTTP REST API @ Port 5000  (siehe contracts/openapi/data-server.v1.yaml)
Client Applications (Dashboard, später ggf. App)
```

| Service        | Ort                   | Sprache    | Verantwortlich für                                            |
|----------------|----------------------|------------|----------------------------------------------------------------|
| Firmware       | Arduino Uno          | C++ (PIO)  | Sensor-Auslesen, Aktoren steuern, Daten via Serial schicken    |
| Data-Server    | Raspberry Pi Zero 2W | Python/Flask | Serial empfangen, in SQLite speichern, REST-API bereitstellen |
| Frontend       | TBD                  | TBD        | Dashboard, Live-Daten, manuelle Steuerung                      |

## Hardware

3 separate Pflanz-Gefäße (Links/Mitte/Rechts) mit je 1 Bodenfeuchte-Sensor; je 1 Pumpe pro Gefäß ist geplant (gebaut ist bisher ein einzelnes Relay an D9). BME280 (Temp/Feuchte/Druck) und BH1750 (Lux) gelten für das ganze Gewächshaus.

Zwei-Spannungs-System: 5V für Arduino, Relay-Steuersignale und Pumpen; 12V für die übrigen Aktoren (Heizmatte, LED-Strips). Gemeinsame Masse erforderlich.

## Querschnittsthemen

- **Graceful Degradation**: Firmware bootet ohne BME280/BH1750.
- **Staleness**: API liefert HTTP 503, wenn die letzte Messung älter als 10 s ist.
- **Auto-Reconnect**: Server reconnected alle 5 s bei Serial-Verbindungsverlust.

## TODO

- [ ] Aktoren-Steuerung beschreiben (Pumpen, Heizmatte, Servo, Pflanzenlicht-Steckdose)
- [ ] Steuerungs-Loop dokumentieren (wer entscheidet wann was?)
- [ ] Persistenz-Strategie (SQLite-Schema, Retention)
