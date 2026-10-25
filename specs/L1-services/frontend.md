# L1 — Frontend (Dashboard)

> Status: Stub. Noch nicht gebaut, hier gesammelt was wir wissen / entscheiden müssen.

## Verantwortung

- Live-Anzeige Sensor-Daten (Temp, Lux, Bodenfeuchte je Gefäß)
- Historische Verläufe (Charts über Stunden / Tage)
- Manuelle Steuerung (Pumpen toggeln, Pflanzenlicht an/aus)
- Alerts bei kritischen Werten (zu trocken, zu heiß, Sensor offline)

## Offene Architektur-Entscheidungen

- [ ] Framework: React / Vue / Svelte / Vanilla JS?
- [ ] Hosting: Auf dem Pi (Flask static) oder separat (Vercel/Netlify)?
- [ ] Real-time: Polling vs. WebSocket vs. SSE?
- [ ] Auth: Lokales Netz only oder erreichbar von außen?
- [ ] Design-System: Eigenes / Tailwind / Component-Library?

## Schnittstellen

| Schnittstelle | Vertrag                                   |
|---------------|-------------------------------------------|
| HTTP REST     | `contracts/openapi/data-server.v1.yaml`   |
