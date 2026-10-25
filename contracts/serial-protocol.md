# Contract: Serial-Protokoll Arduino → Pi

> Status: Stub. Aktuelles Format aus `firmware/src/main.cpp` und `data-server/main.py` (Regex-Parser) ableiten und hier verbindlich festhalten.

## Transport

- Verbindung: USB-Serial (CDC ACM)
- Device auf Pi: `/dev/ttyACM0`
- Baudrate: **9600**
- Encoding: ASCII, Zeilen-getrennt mit `\n`
- Sende-Intervall: alle **2 s** (Best-Effort, kein striktes Real-time)

## Frame-Format (TBD)

Aktuell: strukturierter Text, vom Python-Server per Regex geparst. Abgeleitet aus `greenhouse_v1/src/main.cpp` (Stand `f5261e0`); die Parser-Seite in `data-server/main.py` ist noch nicht abgeglichen.

Eine Zeile pro Intervall, Segmente durch ` | ` getrennt (Werte beispielhaft):

```
Soil_L RAW:431 SMOOTH:428 Moist%:42 | Soil_M RAW:512 SMOOTH:509 Moist%:0 | Soil_R RAW:377 SMOOTH:380 Moist%:71 | Temp:22.4C Humid:55.1% Press:1013hPa | Lux:830
```

- `Soil_<L|M|R>`: Rohwert (ADC), gleitender Mittelwert (N=10), Prozent (0–100, aus `DRY_RAW`/`WET_RAW`).
- `Temp`/`Humid`/`Press`: nur wenn BME280 beim Boot gefunden; 1 bzw. 0 Nachkommastellen.
- `Lux`: nur wenn BH1750 gefunden; bei Lesefehler `Lux:ERROR`.
- Boot-Meldungen und Button-Events laufen über denselben Port — der Empfänger muss Nicht-Frame-Zeilen ignorieren.

## Felder (TBD)

| Feld           | Typ    | Einheit | Quelle    | Optional |
|----------------|--------|---------|-----------|----------|
| temperature    | float  | °C      | BME280    | ja       |
| humidity       | float  | %       | BME280    | ja       |
| pressure       | float  | hPa     | BME280    | ja       |
| lux            | float  | lx      | BH1750    | ja       |
| soil_left      | int    | %       | A2        | nein     |
| soil_mid       | int    | %       | A0        | nein     |
| soil_right     | int    | %       | A3        | nein     |

## Versionierung

Aktuell unversioniert. Regel: **Firmware und Server müssen gemeinsam aktualisiert werden** wenn dieses Dokument sich ändert. Sobald der Vertrag über mehrere Versionen stabil bleiben muss, Versions-Header einführen (`v1: temp=...`).
