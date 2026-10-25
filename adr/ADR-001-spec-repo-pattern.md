# ADR-001: Eigenes Spec-Repo neben den Code-Repos

- **Status:** Akzeptiert
- **Datum:** 2026-04-29

## Kontext

Das Smart-Greenhouse-Projekt besteht aus mehreren unabhängigen Code-Repos (`greenhouse_v1`/Firmware, `data-server`, später Frontend). Architektur-Entscheidungen, Schnittstellen und Konventionen waren bisher in `CLAUDE.md` und `docs/` des "Arduino"-Workspace-Ordners verstreut. Mit wachsendem Umfang (mehr Services, mehr Features) wird das unübersichtlich, und zentrale Verträge wie das Serial-Protokoll oder die REST-API leben in keinem Repo wirklich verbindlich.

Sekundäres Ziel: das Setup ist ein **POC**, um ein Spec-First-Setup über mehrere Repos in einem überschaubaren, privaten Projekt auszuprobieren.

## Entscheidung

Wir legen ein eigenes Repo `greenhouse-specs` an, das parallel zu den Code-Repos in einem gemeinsamen Workspace-Ordner (`~/Documents/greenhouse/`) liegt. Konsumiert wird per **Pattern A — Workspace-Klon**: alle Repos werden lokal nebeneinander gecheckt out, Claude Code wird auf den Workspace-Ordner gestartet und sieht dadurch Specs und Code gleichzeitig.

Inhalte des Spec-Repos:

- **`specs/`** — High-Level-Architektur, pro Service eine L1-Spec, pro Feature eine L2-Spec
- **`contracts/`** — Maschinenlesbare Verträge (OpenAPI, JSON Schemas, Serial-Protokoll-Doc)
- **`adr/`** — Architecture Decision Records
- **`conventions/`** — Coding-Standards und Cross-Repo-Guidelines (`AGENTS.md`)
- **`glossary.md`** — Domänensprache

Bewusst **nicht** im Spec-Repo: Code, generierte Artefakte (z. B. OpenAPI-Clients), Secrets, Service-spezifische Implementierungs-Details.

## Konsequenzen

**Positiv:**
- Eine klare Heimat für service-übergreifende Verträge.
- Claude Code kann zur Implementierungs-Zeit die Spec direkt referenzieren.
- Der POC zeigt im Kleinen, wie gut Spec-First über mehrere Repos trägt.

**Negativ:**
- Drei Repos statt zwei → mehr `git pull`-Disziplin.
- Risiko, dass Specs und Code auseinanderlaufen (Drift). Gegenmaßnahme im POC: aktiv beobachten, ob Drift auftritt, und ggf. Lint/CI-Prüfungen einführen.
- Versionierung der Specs aktuell nicht vorgesehen — alle Konsumenten arbeiten gegen `main`. Reicht für 1 Dev / 2 Repos; bei mehr Entwicklern oder Services möglicherweise nicht (siehe folgende ADRs).

## Alternativen

- **Monorepo mit `specs/`-Unterordner**: Einfacher, aber wir wollen den Multi-Repo-Pattern explizit testen.
- **Specs in jedem Code-Repo duplizieren**: Klassische Drift-Hölle, abgelehnt.
- **Specs nur in CLAUDE.md**: Funktioniert für 1 kleines Repo, skaliert nicht auf mehrere Services.
