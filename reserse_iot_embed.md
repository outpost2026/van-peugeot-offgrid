# IoT embed zařízení s high EROI — monitoring a automatizace off-grid systému

## 1. Monitoring Victron zařízení (VE.Direct / BLE)

### 1.1 ESP32 + VE.Direct kabel (nejvyšší EROI)

| Parametr | Hodnota |
|---|---|
| Náklady | ~150–250 Kč (ESP32 + VE.Direct kabel/alza kabel) |
| Přínos | Reálný čas: napětí baterie, proud, SOC, výkon FV, stav MPPT, Orion XS |
| EROI | **★★★★★** — okamžitý přehled o celém systému |

- **ESPHome komponenta (doporučeno):** `syssi/esphome-victron-vedirect` (github.com/syssi/esphome-victron-vedirect) nebo `KinDR007/VictronMPPT-ESPHOME`
- Podporuje: MPPT SmartSolar, SmartShunt, BMV, Orion XS, Phoenix Inverter
- Čte: Vpanel, Vbatt, Ibatt, Ppv, SOC, TTG, error kódy, režimy nabíjení
- Data přímo do Home Assistant bez Victron cloudu
- **Galvanické oddělení:** ADUM1201 (doporučeno, ~50 Kč) pro ochranu Victron zařízení

**Minimální konfigurace (ESPHome):**
```yaml
uart:
  rx_pin: GPIO16
  baud_rate: 19200

external_components:
  - source: github://KinDR007/VictronMPPT-ESPHOME@main

victron:
  id: victron0

sensor:
  - platform: victron
    victron_id: victron0
    battery_voltage:
      name: "Baterie napětí"
    battery_current:
      name: "Baterie proud"
    panel_power:
      name: "FV výkon"
    state_of_charge:
      name: "Stav nabití (SoC)"
```

### 1.2 ESP32 + BLE (bez kabelu)

| Parametr | Hodnota |
|---|---|
| Náklady | ~150 Kč (ESP32) |
| Přínos | Monitoring bez drátu, pasivní příjem BLE reklam |
| EROI | **★★★★☆** — bez kabeláže, ale jen data z BLE broadcastu |

- **ESPHome komponenta:** `Fabian-Schmidt/esphome-victron_ble` (github.com/Fabian-Schmidt/esphome-victron_ble)
- Potřebuje MAC adresu + bindkey z VictronConnect (Instant Readout)
- Podporuje: SmartSolar, SmartShunt, Orion XS, SmartLithium, Lynx Smart BMS
- Čte: V, I, P, SOC, TTG, cell voltages (LiFePO₄), alarmy
- Lze kombinovat s BLE proxy pro rozšíření dosahu

**Důležité:** Klient má MultiPlus C (bez BLE) — ten nelze monitorovat BLE. Ale MPPT 100/50 a Orion XS mají BLE.

### 1.3 OpenDTU-OnBattery — Victron + Hoymiles v jednom

| Parametr | Hodnota |
|---|---|
| Náklady | ~300 Kč (ESP32 + VE.Direct kabel) |
| Přínos | Řízení výroby + monitoring baterie |
| EROI | **★★★★☆** — pokud bude v budoucnu solární mikroinvertor |

- github.com/scho0ck/OpenDTU-OnBattery
- Kombinuje monitoring Victron MPPT (VE.Direct) + řízení Hoymiles mikroinvertorů
- Dynamické omezení výkonu dle spotřeby (zero feed-in)
- Podpora Pylontech BMS přes CAN bus

---

## 2. Detekce plynů (CO + LPG) — bezpečnost

### 2.1 ESP32 + MQ-7 (CO) + MQ-2 (LPG)

| Parametr | Hodnota |
|---|---|
| Náklady | ~250–350 Kč (ESP32 + 2× senzor + OLED) |
| Přínos | Detekce CO z naftového topení + LPG z vaření |
| EROI | **★★★★★** — levnější než komerční detektory, integrovaný do HA |

- **MQ-7** — detekce CO (0–1000 ppm), citlivý na 50–200 ppm (ideální pro topení)
- **MQ-2** — detekce LPG, propanu, metanu (0–10000 ppm)
- **DHT22** — teplota + vlhkost (~50 Kč)
- **OLED SSD1306** — lokální zobrazení (~60 Kč)
- Data do Home Assistant přes ESPHome, notifikace při překročení prahů
- **ESPHome nativní** — `sensor` platforma pro MQ-x senzory

**Konfigurace (ESPHome):**
```yaml
sensor:
  - platform: mq7
    pin: A0
    name: "CO koncentrace"
  - platform: mq2
    pin: A1
    name: "LPG koncentrace"
  - platform: dht
    pin: D2
    temperature:
      name: "Teplota"
    humidity:
      name: "Vlhkost"
```

**Upozornění:** MQ senzory potřebují ~48h zahřátí na stabilní hodnoty a kalibraci R₀ na čistém vzduchu. Nejsou přesné jako NDIR, ale pro bezpečnostní prahování dostačující.

### 2.2 Komerční alternativa s IoT výstupem

- **Shelly Gas** (~600 Kč) — detekce zemního plynu/LPG, WiFi, notifikace
- **Nest Protect / Xiaomi Honeywell** — kouř + CO, dražší, bez přímé HA integrace
- Doporučení: ESP32 + MQ senzory jako doplňková vrstva k certifikovaným detektorům

---

## 3. Teplotní monitoring (DS18B20)

| Parametr | Hodnota |
|---|---|
| Náklady | ~40–80 Kč/senzor (DS18B20 v kovovém pouzdře) |
| Přínos | Monitoring teploty baterie, kabelů, měniče, pojistek |
| EROI | **★★★★★** — nejlevnější smysluplný senzor |

- **DS18B20** — digitální, 1-Wire, rozsah -55 až +125°C, přesnost ±0.5°C
- Lze připojit až 8+ senzorů na jeden GPIO pin
- **Doporučená místa v projektu Kuby:**
  - Na baterii Wattcycle (BMS už má vnitřní čidlo, ale externí pro kontrolu)
  - Na kabeláži (50mm² trunk, Lynx Distributor)
  - Na MultiPlus C (teplota měniče)
  - Vnitřní teplota dodávky (uvidíš účinnost vytápění)
- Data do HA → automatizace (vypínání při přehřátí, alerty)

**Konfigurace (ESPHome):**
```yaml
sensor:
  - platform: dallas
    address: 0x1c0000031e1234
    name: "Teplota baterie"
  - platform: dallas
    address: 0x1c0000031e5678
    name: "Teplota MultiPlus"
```

---

## 4. Měření proudu a výkonu 230V

### 4.1 PZEM-004T v3 (doporučeno)

| Parametr | Hodnota |
|---|---|
| Náklady | ~250–350 Kč (PZEM-004T + ESP32) |
| Přínos | Měří V, I, P, kWh, PF, freq — vše na 230V straně |
| EROI | **★★★★☆** — kompletní AC monitoring za pár korun |

- Měří: 80–260V, 0–100A, 0–23kW, kWh, power factor, frekvence
- Komunikace: Modbus-RTU přes UART (TX/RX)
- Přesnost: ±0.5% (billing-grade)
- **V projektu Kuby:** monitoring zásuvky AC-OUT — kolik odebíráš z MultiPlusu
- ESPHome nativní komponenta `pzemac` / `pzemdc`

### 4.2 SCT-013 (non-invazivní CT kleště)

| Parametr | Hodnota |
|---|---|
| Náklady | ~100–150 Kč (SCT-013-000 + pár rezistorů) |
| Přínos | Měření AC proudu bez zásahu do kabeláže |
| EROI | **★★★☆☆** — levné, ale jen proud (bez V nelze výkon) |

- SCT-013-000 (100A) — výstup 0–50mA, potřebuje burden resistor
- SCT-013-030 (30A) — výstup 0–1V, lze připojit přímo
- True RMS přes EmonLib nebo ESPHome `ct_clamp`
- **Pozor:** Nelze měřit DC — jen pro AC stranu

---

## 5. Display a lokální UI

### 5.1 OLED SSD1306 128×64

| Parametr | Hodnota |
|---|---|
| Náklady | ~60–100 Kč |
| Přínos | Okamžitý přehled bez nutnosti otevřít telefon |
| EROI | **★★★★☆** — levný, jednoduchý, velký přínos |

- I²C (4 piny) nebo SPI
- ESPHome nativní `display` platforma
- Zobrazí: Vbatt, Ibatt, SoC, PV výkon, teploty, stav MPPT
- Lze umístit do rozvaděče nebo na viditelné místo v dodávce

### 5.2 Nextion displej (pokročilé)

| Parametr | Hodnota |
|---|---|
| Náklady | ~400–800 Kč |
| Přínos | Dotykový panel s vlastním procesorem a UI |
| EROI | **★★★☆☆** — dražší, ale působí profesionálně |

- Sériová komunikace s ESP32
- Vlastní editor (Nextion Editor) pro tvorbu UI
- Možnost ovládat spotřebiče

---

## 6. Architektura a integrace

### 6.1 ESPHome jako standard

Všechna zařízení doporučuji postavit na **ESPHome** — jednotný framework, který:
- Automaticky publikuje data do Home Assistant
- Podporuje OTA aktualizace
- Dává senzory, binary sensory, text sensory, spínače, čísla
- Nízká režie (ESP8266 stačí na jednoduchá čidla)

**Topologie:**
```
┌──────────────────────────────────────────────────────┐
│                  Dodávka (LAN/WiFi)                   │
│                                                       │
│  ESP32-1 (Victron VE.Direct)  →  MPPT, SmartShunt    │
│  ESP32-2 (Safety)             →  MQ-7, MQ-2, DHT22   │
│  ESP32-3 (Temperature)        →  DS18B20 × 4         │
│  ESP32-4 (AC Monitor)         →  PZEM-004T           │
│                                                       │
│  ┌──────────┐                                        │
│  │  Router  │◄── WiFi                                 │
│  └────┬─────┘                                        │
│       │                                               │
│  ┌────▼─────┐                                        │
│  │  HA/NUC  │  ←  ESPHome API / MQTT                  │
│  └──────────┘                                        │
└──────────────────────────────────────────────────────┘
```

### 6.2 Alternativa: jeden ESP32 na vše

Pro minimalistický setup stačí jeden ESP32:
- UART1: VE.Direct → MPPT nebo SmartShunt (ale klient nyní nemá SmartShunt)
- UART2: PZEM-004T
- GPIO: DS18B20 × ?, MQ-7, MQ-2, OLED

**Cena celkem:** ~500–700 Kč za jeden ESP32 + všechna čidla

---

## 7. Celkové shrnutí — EROI ranking

| # | Zařízení | Cena | Přínos | EROI |
|---|---|---|---|---|
| 1 | **DS18B20** (×4) | ~200 Kč | Teplota baterie, kabelů, měniče — prevence přehřátí | ★★★★★ |
| 2 | **ESP32 + VE.Direct** | ~250 Kč | Monitoring Victron MPPT/Orion v reálném čase v HA | ★★★★★ |
| 3 | **ESP32 + MQ-7 + MQ-2** | ~300 Kč | Detekce CO + LPG — bezpečnost, alerty do HA | ★★★★★ |
| 4 | **OLED SSD1306** | ~60 Kč | Lokální zobrazení klíčových hodnot | ★★★★☆ |
| 5 | **PZEM-004T** | ~250 Kč | Monitoring AC výkonu (kWh, W, A, V) | ★★★★☆ |
| 6 | **ESP32 + BLE Victron** | ~150 Kč | Bezdrátový monitoring (jen broadcast data) | ★★★★☆ |
| 7 | **SCT-013 + ESP32** | ~150 Kč | AC proud bez kontaktu (jen A, bez W) | ★★★☆☆ |
| 8 | **OpenDTU-OnBattery** | ~300 Kč | Řízení mikroinvertorů + monitoring MPPT | ★★★☆☆ |
| 9 | **Nextion displej** | ~600 Kč | Profesionální UI, dotykové ovládání | ★★★☆☆ |

**Nejvyšší priorita pro projekt:**
1. ESP32 + VE.Direct kabel → monitoring MPPT (až bude k dispozici)
2. DS18B20 na baterii a kabeláž (prevence)
3. MQ-7 (CO) pro bezpečnost u naftového topení

---

## 8. Zdroje

- **ESPHome Victron VE.Direct:** https://github.com/syssi/esphome-victron-vedirect
- **ESPHome Victron MPPT:** https://github.com/KinDR007/VictronMPPT-ESPHOME
- **ESPHome Victron BLE:** https://github.com/Fabian-Schmidt/esphome-victron_ble
- **OpenDTU-OnBattery:** https://github.com/scho0ck/OpenDTU-OnBattery
- **Victron VE.Direct HEX control:** https://github.com/AcMetelka/esphome-ve-direct-hex
- **ESPHome DS18B20:** https://esphome.io/components/sensor/dallas.html
- **ESPHome PZEM:** https://esphome.io/components/sensor/pzemac.html
- **ESPHome CT Clamp:** https://esphome.io/components/sensor/ct_clamp.html
- **ESP32 gas safety monitoring:** https://github.com/P-P-programer/Multi-Gas-Safety-System-with-Voice-Alerts-Web-Dashboard
- **ESPHome MQ7:** https://esphome.io/components/sensor/mq7.html
- **ESP32 PZEM tutorial:** https://www.michaelstinkerings.org/building-a-power-monitoring-system-with-esp32-and-pzem-004t-a-pull-based-approach/
- **Victron BLE library pro ESP32/nRF52:** https://github.com/SH3D/VictronBLE

---

*Dokument generated 2026-07-08*
