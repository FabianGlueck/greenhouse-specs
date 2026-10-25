# F001 — Automatische Bewässerung

> Status: Entwurf. Bestehende Hardware-/Software-Checkliste in `~/Documents/greenhouse/docs/aufgaben/01-bewaesserung.md` migrieren.

## Ziel

Automatisches Gießen pro Gefäß, sobald die Bodenfeuchte unter einen konfigurierbaren Schwellwert fällt.

## Akzeptanzkriterien

- [ ] Pro Gefäß ein eigener Schwellwert konfigurierbar (Basilikum ≠ Salat ≠ Kresse)
- [ ] Pumpe läuft nur für konfigurierbare Dauer (Über-Bewässerungsschutz)
- [ ] Mindestabstand zwischen zwei Gieß-Vorgängen pro Gefäß (z. B. 30 min)
- [ ] Manueller Override per Button bleibt jederzeit möglich
- [ ] Notabschaltung: Wenn Bodenfeuchte trotz Pumpen nicht steigt → Pumpe stoppen, Alert

## Offene Fragen

- Wer steuert: Arduino autonom oder Pi sendet Befehl?
- Gieß-Dauer: feste Sekunden oder feedback-loop bis Zielfeuchte?
- Wie wird "Wassertank leer" erkannt? Float-Switch oder über Feuchte-Verlauf?

## TODO

- [ ] Inhalte aus `docs/aufgaben/01-bewaesserung.md` hierher migrieren
- [ ] Schwellwerte pro Pflanze recherchieren
- [ ] Steuerungs-Verantwortung entscheiden (siehe oben)
