# KS1C – Kammerheizung (ESPHome + Home Assistant)

🔥 **ESP32-basierte Kammerheizung für geschlossene 3D-Drucker**  
Mit automatischer Temperaturregelung, Sicherheitsfunktionen, Display
und direkter Integration in **Home Assistant** und **Moonraker**.

---

## 📸 Projektbilder

> 💡 Lege deine Bilder z. B. unter `docs/images/` im Repository ab  
> und passe die Dateinamen bei Bedarf an.

### Dashboard
![Dashboard](Bilder/HA-Dashboard.png)

---

## ✨ Features

- ESP32 (TTGO T-Display) mit integriertem TFT-Display
- Temperaturregelung für geschlossene Druckkammern
- Zwei **Solid State Relais (SSR)** für:
  - Heizung (230 V)
  - Kammerlüfter (230 V)
- **Taktbetrieb** für überdimensionierte Heizungen
- Lüfter-Vorlauf & Nachlauf
- **Not-Aus**, Übertemperaturschutz & WLAN-Failsafe
- Native **ESPHome-Integration**
- **Moonraker-Anbindung** für MMU-Dryer-Status
- Vollständig lokal, kein Cloud-Zwang

---

## 🧠 Systemübersicht

Dieses Projekt ist strikt in **zwei Spannungsbereiche** getrennt:

| Bereich | Spannung | Beschreibung |
|------|--------|-------------|
| Niederspannung | 3,3 V DC | ESP32, Sensoren, SSR-Eingänge |
| Netzspannung | 230 V AC | Heizung, Lüfter |

👉 Die Trennung erfolgt **ausschließlich über Solid State Relais**.

---

## 🧰 Verwendete Hardware (exakt)

### 1️⃣ ESP32 Controller
**LILYGO TTGO T-Display (ESP32 + ST7789)**  
🔗 https://www.amazon.de/dp/B099MPFJ9M  

- ESP32 Microcontroller
- 1.14" TFT Display (135×240)
- 3,3 V GPIO
- USB-C (CH9102F)

---

### 2️⃣ Solid State Relais (2×)
**BGTXINGI SSR-40DA**  
🔗 https://www.amazon.de/dp/B09NDFDLLN  

| SSR | Funktion |
|----|---------|
| SSR #1 | Schaltet die Kammer-Heizung |
| SSR #2 | Schaltet den Kammer-Ventilator |

- Steuereingang: 3–32 V DC (ESP32-kompatibel)
- Lastseite: 24–380 V AC
- Geräuschlos, kein Verschleiß

---

### 3️⃣ Heizelement
**PTC-Heizung 230 V / 300 W mit Lüfter**  
🔗 https://www.amazon.de/dp/B09XV41P7L  

- Selbstregelndes PTC-Element
- Wird über SSR #1 geschaltet
- Temperaturregelung über ESPHome-Logik

---

## 🔌 GPIO-Belegung (ESP32)

| GPIO | Funktion |
|----|--------|
| GPIO25 | SSR Heizung |
| GPIO26 | SSR Lüfter |
| GPIO21 | I²C SDA (BMP280) |
| GPIO22 | I²C SCL (BMP280) |
| 3.3 V | Sensor-Versorgung |
| GND | SSR-Eingänge (–) |

---

## 🧯 Sicherheitsfunktionen

- ❌ **Übertemperatur > 65 °C** → Sofortige Abschaltung
- 📡 **WLAN-Ausfall** → Hard-Shutdown + manuelle Entsperrung nötig
- 🛑 **Not-Aus** → Heizung AUS, Lüfter EIN
- 🌀 **Lüfter-Nachlauf** nach Heizende
- ⏱ Sensor-Grace-Phase beim Booten

---

## 🏠 Home Assistant Integration

- Native **ESPHome-Integration**
- Alle Sensoren, Schalter & Zahlen als Entities
- Anzeige von:
  - Kammer-Temperatur
  - Heizstatus
  - Lüfter-Nachlauf
  - Sicherheitszustand

---

## 🧩 Moonraker Integration (optional, aber empfohlen)

Für MMU-Dryer-Status & Temperatur:

🔗 **Moonraker Home Assistant Plugin**  
https://github.com/marcolivierarsenault/moonraker-home-assistant

---

## 🚀 Erste Inbetriebnahme (Kurzfassung)

1. ESP32 **ohne 230 V** flashen und testen  
2. Temperaturwerte in Home Assistant prüfen  
3. SSR-Eingänge testen (LEDs / Schalten)  
4. Erst dann Netzspannung anschließen  
5. Ersten Heizzyklus beobachten

---

## ⚠️ Wichtiger Hinweis

Dieses Projekt arbeitet mit **230 V Netzspannung**.  
Falsche Verdrahtung kann **lebensgefährlich** sein.

> ❗ Nachbau nur, wenn du weißt, was du tust.  
> ❗ Immer Sicherungen, Erdung und Gehäuse verwenden.

---

## 📄 Lizenz

Dieses Projekt ist für private Nutzung gedacht.  
Siehe `LICENSE` Datei für Details.

---

## Credits

Projekt & Umsetzung: **jeng37**  
ESPHome • Home Assistant • Moonraker Community
