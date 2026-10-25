# ADR-002: Multi-Repo (Code) + Single Spec-Repo

- **Status:** Akzeptiert
- **Datum:** 2026-04-29

## Kontext

Bestehender Stand: Firmware (`greenhouse_v1`) und Backend (`data-server`) leben bereits in eigenen GitHub-Repos. Frage war: Konsolidieren wir zu einem Monorepo, oder bleiben es separate Repos?

## Entscheidung

Wir behalten **separate Code-Repos** und ergänzen sie um ein gemeinsames **Spec-Repo** (siehe ADR-001).

## Begründung

- **Unterschiedliche Toolchains**: PlatformIO (C++) vs. uv/Python — kein gemeinsames Build-System nötig.
- **Unterschiedliche Deploy-Pfade**: Firmware → avrdude flash; Server → git pull auf dem Pi. Eine Codebase, zwei Pipelines wäre unnötig komplex.
- **Existierender Stand**: Beide Repos sind bereits etabliert mit eigener History — Konsolidierung ohne klaren Nutzen.
- **POC-Wert**: Das Projekt soll gerade das Zusammenspiel mehrerer Repos über ein Spec-Repo erproben. Die Erfahrung damit ist hier explizit gewünscht.

## Konsequenzen

- Cross-Repo-Refactorings (z. B. Schnittstellen-Änderung, die Firmware und Server gleichzeitig betrifft) erfordern Koordination zwischen mehreren PRs.
- Specs sind die einzige Stelle, an der Cross-Repo-Verträge verbindlich werden — daher das Spec-Repo.
