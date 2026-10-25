# L1 — Firmware (Arduino Uno)

> Status: Stub. Zu befüllen.

## Verantwortung

- Sensoren auslesen (3× Bodenfeuchte, BME280, BH1750)
- Werte glätten (Moving Average)
- Aktoren steuern (geplant: Pumpen via Relay, später Heizmatte, Servo — aktuell wird das Relay auf D9 nur initialisiert, nicht geschaltet)
- Daten alle 2 s über USB-Serial an den Pi senden
- Buttons als manuelle Override-Steuerung (geplant — aktuell schalten sie nur die LED auf D8)

## Schnittstellen

| Schnittstelle | Richtung   | Vertrag                                  |
|---------------|------------|------------------------------------------|
| USB-Serial    | TX → Pi    | `contracts/serial-protocol.md`           |
| USB-Serial    | RX ← Pi    | TBD (Steuerungsbefehle vom Server)       |

## Pin-Belegung

Quelle of truth ist `firmware/src/main.cpp`. Hier nur Übersicht.

**Gebaut** (Stand `greenhouse_v1` `f5261e0`):

| Pin    | Funktion                                  |
|--------|--------------------------------------------|
| A0     | Bodenfeuchte Mitte                         |
| A2     | Bodenfeuchte Links                         |
| A3     | Bodenfeuchte Rechts                        |
| A4/A5  | I2C (BME280, BH1750)                       |
| D8     | Externe LED                                |
| D9     | Relay-Eingang (ein Kanal, nur initialisiert) |
| D10–D12| Buttons (schalten aktuell die LED)         |

**Geplant** (noch nicht gebaut):

| Pin    | Funktion                          |
|--------|------------------------------------|
| D2     | Relay Pumpe Links                  |
| D3     | Relay Pumpe Mitte                  |
| D4     | Relay Pumpe Rechts                 |
| D10–D12| Buttons als manueller Pump-Toggle  |

## Nicht-funktionale Anforderungen

- Boot-Robustheit: Auch ohne BME280/BH1750 lauffähig (Graceful Degradation via I2C-Scan).
- Determinismus: Sende-Intervall 2 s, kein Drift > 50 ms erwartet.
- Kein dynamisches Memory-Allocation auf der Uno (2 KB SRAM).

## TODO

- [ ] Steuerungs-Befehle vom Pi empfangen können (Format definieren)
- [ ] Bewässerungs-Logik (siehe F001)
- [ ] Heizmatten-Steuerung (siehe spätere Feature-Spec)
