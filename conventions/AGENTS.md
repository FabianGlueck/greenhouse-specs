# AGENTS.md — Coding-Standards (Cross-Repo)

Konventionen für Claude Code beim Arbeiten am Smart-Greenhouse-Projekt. Gilt für alle Code-Repos im Workspace.

## Allgemein

- **Spec-First**: Bei Änderungen an einer Schnittstelle (Serial, REST) zuerst die zugehörige Datei in `greenhouse-specs/contracts/` aktualisieren, dann den Code.
- **CLAUDE.md pro Repo bleibt schlank**: Nur Repo-spezifische Hinweise (Build-Befehle, Pin-Belegung). Architektur und Cross-Cutting → Spec-Repo.
- **Sprache**: Code-Kommentare und User-facing Strings auf Englisch. Specs, ADRs und Commits gerne Deutsch (Projekt-Sprache).
- **Keine Erfindungen**: Wenn eine Spec "TBD" sagt, **nicht** rateweise Werte einsetzen — nachfragen.

## Firmware (Arduino, C++)

- Kein dynamisches Memory-Allocation (`new`, `malloc`, `String`-Konkatenation in Loops).
- Pin-Konstanten als `#define` oder `constexpr` am Datei-Anfang.
- Sensor-Initialisierung defensiv: I2C-Scan, Graceful Degradation bei Fehler.

## Data-Server (Python, Flask)

- Package-Manager: `uv` (kein `pip install` direkt).
- Serial-Zugriff immer via `serial_lock`.
- Neue API-Endpunkte zuerst in `contracts/openapi/data-server.v1.yaml` aufnehmen.

## Commits

- Format: kurze, imperative Subject-Line. Body optional.
- Bei Cross-Repo-Änderungen den ADR oder die Spec im Body referenzieren (Pfad reicht, kein URL-Aufwand).

## Was NICHT tun

- Keine generierten Artefakte committen (z. B. OpenAPI-Clients).
- Keine Secrets/Tokens im Code (auch nicht in Beispielen).
- Keine Backwards-Compat-Shims im POC — wir können breaking changes machen, weil 1 Dev und 2 Konsumenten.
