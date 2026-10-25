# F002 — Web-Dashboard

> Status: Stub. Noch nicht angefangen.

## Ziel

Einfaches Web-Dashboard zur Live-Anzeige der Sensor-Daten und manuellen Steuerung.

## Akzeptanzkriterien

- [ ] Live-Werte (Temp, Lux, Bodenfeuchte je Gefäß) mit < 5 s Verzögerung
- [ ] Historischer Chart (24 h, 7 d) pro Sensor
- [ ] Visueller Stale-Indikator wenn Daten älter als 10 s
- [ ] Manuelles Pump-Toggle pro Gefäß
- [ ] Mobile-First (wird hauptsächlich auf dem Handy bedient)

## Offene Fragen

Siehe `specs/L1-services/frontend.md` — Framework, Hosting, Real-time-Strategie noch zu entscheiden.

## TODO

- [ ] Wireframe / Skizze
- [ ] ADR für Framework-Wahl
- [ ] Endpunkt für manuelle Steuerung im data-server spezifizieren
