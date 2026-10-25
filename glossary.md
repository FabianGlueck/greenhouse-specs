# Glossar

Begriffe und Domänensprache. Wenn du dich beim Schreiben einer Spec dabei ertappst, einen Begriff erklären zu wollen — er gehört hierher.

| Begriff | Bedeutung |
|---------|-----------|
| Gefäß | Eines der drei Pflanz-Abteile (Links / Mitte / Rechts). Jedes hat einen eigenen Bodenfeuchte-Sensor; eine eigene Pumpe pro Gefäß ist geplant. |
| Bodenfeuchte-Sensor | Kapazitiver Sensor, gibt Rohwert 0–1023 zurück. Wird per `DRY_RAW`/`WET_RAW` in Prozent umgerechnet (aktuell ein gemeinsames Wertepaar für alle drei Sensoren). |
| `DRY_RAW` / `WET_RAW` | Kalibrierungswerte: ADC-Wert bei trockenem bzw. nassem Substrat (aktuell 500 / 330, für alle Sensoren gleich; Kalibrierung pro Sensor geplant). |
| Moving Average | Gleitender Mittelwert über die letzten N Messwerte (aktuell N=10), zur Glättung von Sensor-Rauschen. |
| Relay | 4-Kanal-Modul. Gebaut: ein Steuereingang an D9. Geplant: je eine Pumpe pro Gefäß über D2/D3/D4 (5V-Pumpen, siehe `specs/L0-architecture.md`). |
| Graceful Degradation | Firmware bootet auch ohne BME280/BH1750; fehlende Sensoren werden via I2C-Scan erkannt und ihre Felder nicht gesendet. |
| Serial-Protokoll | Strukturiertes Text-Format, das die Firmware alle 2 s über USB-Serial an den Pi schickt. Siehe `contracts/serial-protocol.md`. |
| Stale Reading | Letzte Messung ist >10 s alt — API antwortet mit HTTP 503. |
| Workspace | Lokales Dach-Verzeichnis (`~/Documents/greenhouse/`), das Spec-Repo und Code-Repos enthält. |
