<div align="left">
  <a href="https://github.com/outpost2026/van-peugeot-offgrid/blob/main/README.md">
    <img src="https://flagcdn.com/24x18/cz.png" alt="CZ" height="18"> Česky
  </a>
</div>

# ⚡ Peugeot Boxer 2021 Campervan Off-Grid Electrification — 12V/230V

**Victron Energy off-grid system for a Peugeot Boxer L4H2 campervan conversion.**  
Minimalist setup: 12V compressor fridge, MaxxFan roof vent, USB charging ports, one 230V socket, alternator charging + future solar.

> 🇨🇿 This is the English version for the international van conversion community.  
> The project documentation and client communications are in Czech.

---

## System Architecture

```
Alternator (Euro6) → Orion XS 50A ─┐
                                    ├── Lynx Distributor M10 ←── Battery Wattcycle 314Ah
Solar panel AIKO 445W → MPPT 100/50┘           │
                                          ┌─────┴──────┐
                                     MultiPlus C       12V distribution block
                                    12/1600/70-16      │──├ LED lights
                                          │            │──├ USB/12V sockets
                                     AC distribution   │──├ 12V fridge
                                     ├── 230V socket   │──├ MaxxFan roof vent
                                     ├── floor heating │──├ Diesel heater
                                     └── water heater  └──├ Water pump (future)
```

## Why This Build?

The client wanted a **simple, reliable, and expandable** electrical system for his Peugeot Boxer 2021 campervan conversion. The system is built around industry-standard Victron Energy components with a WattCycle 314Ah LiFePO₄ battery as the energy storage.  

Key requirements:
- Minimalist setup — only essential 12V loads + one 230V socket
- Alternator charging via DC-DC (mandatory for Euro6 smart alternator)
- Solar-ready (panel not yet installed)
- Shore power connection with PowerAssist
- Expandable for future additions (water system, full AC distribution, IoT monitoring)

## Components

| Component | Specification | Role |
|---|---|---|
| **Battery** | Wattcycle 12V 314Ah Mini LiFePO₄ (200A BMS, ~4 kWh usable ~3.2 kWh) | Main energy storage — Grade-A cells, aluminum case for vibration resistance |
| **Inverter/Charger** | Victron MultiPlus C 12/1600/70-16 (1300W cont. / 3000W peak, 70A charger, 16A transfer) | System core: inverter, battery charger, AC transfer switch, PowerAssist |
| **DC-DC Charger** | Victron Orion XS 12/12-50A (50A, fanless, Bluetooth) | Alternator charging while driving — mandatory for Euro6 smart alternator (variable voltage) |
| **Solar Charger** | Victron SmartSolar MPPT 100/50 (100V max input, 50A output, Bluetooth) | Solar charge controller for future AIKO panel |
| **Solar Panel** | AIKO Nebular 445W lightweight (8.6 kg, Voc ~40V, Isc ~14A) | Future — not yet installed |
| **DC Distribution** | Victron Lynx Distributor M10 (1000A busbar, 4× MEGA fuse positions) | Central DC distribution + fuse protection |
| **12V Distribution** | K735A distribution block (12 ways, blade fuses) | Distribution to 12V loads |

## Key Design Decisions

### 1. Orion XS Grounding — GND → Chassis (NOT battery negative)

This is **critical** and follows Victron's RV SYSTEM 3 wiring scheme. The Orion XS is a **non-isolated** DC-DC charger — its GND terminal must go to the vehicle chassis, NOT to the Lynx Distributor negative bus and NOT to the starter battery negative. The chassis carries the return current (~2A) during charging. This is the most common wiring mistake in van builds.

### 2. MultiPlus Ground Relay = ON

Required for the RCD (residual current device) to function in inverter (off-grid) mode. Configured via VEConfigure / VE.Bus Smart dongle.

### 3. PowerAssist

MultiPlus supplements insufficient shore power (e.g., a 6A campsite outlet) with battery power when a high-load appliance kicks in. This is a key Victron feature for van life.

### 4. Double-Pole 230V Everything

Campsite electricity can have live/neutral reversed. All AC protection (RCBO, RCD, MCBs) must switch **both poles**.

### 5. Cable Sizing — 50mm² Main DC Trunk

The battery↔Lynx↔MultiPlus trunk uses **50mm²** (AWG 0) cable. This is sized for the ~130–160A load (not voltage drop — the run is only ~20-40cm). Victron specifies 35mm² stock / 70mm² for 1.5–5m runs. 50mm² provides headroom above the 200A Mega fuse.

## Wiring Specifications

| Circuit | Gauge | Protection |
|---|---|---|
| Battery ↔ Lynx / MultiPlus | 50mm² (AWG 0) | MEGA 200A |
| Lynx− → chassis ground | 50mm² (AWG 0) | — |
| MPPT ↔ Lynx Distributor | 16mm² (AWG 6) | MEGA 60A |
| Orion XS (IN/OUT/GND) | 16mm² (AWG 6) | MEGA 60A (both sides) |
| 12V block ↔ Lynx | 16mm² (AWG 6) | MEGA 60A |
| Solar panel → MPPT (PV) | 6mm² (AWG 10) | DC disconnect C20 |
| 12V fridge | 6mm² (AWG 10) | blade 15A |
| Diesel heater | 6mm² (AWG 10) | blade 20A |
| USB/12V sockets | 2.5mm² (AWG 14) | blade 10A |
| LED lights | 1.5mm² (AWG 16) | blade 10A |
| MaxxFan roof vent | 1.5mm² twisted pair | blade 5A |
| 230V socket | 3×2.5mm² | MCB 16A |
| PE → chassis | 6mm² green-yellow | — |

## Project Status (July 2026)

| Owned ✅ | To Purchase ❓ | Future 🔮 |
|---|---|---|
| Wattcycle 314Ah battery | Lynx Distributor M10 | AIKO 445W solar panel |
| MultiPlus C 12/1600/70-16 | MEGA fuses (2×200A, 4×60A) | Water system (pump + boiler) |
| Orion XS 12/12-50A | AC protection (RCBO, RCD, MCB) | IoT monitoring (ESPHome) |
| Hydraulic crimping tool | Cables (50/16/6mm²) | |
| Battery Switch 275A | 12V fridge, MaxxFan, lights | |
| Peugeot Boxer 2021 | VE.Bus Smart dongle | |

## Timeline

1. **2026-07-09** — Client consultation (physical component inspection, final design sign-off, terms)
2. **Procurement** — Purchase missing components (Lynx, fuses, cables, AC protection)
3. **Installation** — Lynx Distributor mounting → DC wiring → AC wiring → MultiPlus VEConfigure → Testing
4. **Expansion** — Solar panel installation, IoT monitoring (ESP32 + VE.Direct + ESPHome + Home Assistant)

## Vehicle Background — Peugeot Boxer 2021

- **Model:** Peugeot Boxer L4H2 (long wheelbase, high roof)  
- **Engine:** 2.2 BlueHDi Euro6 — **smart alternator** (variable voltage, ECU-controlled)  
- **Implication:** A DC-DC charger (Orion XS) is mandatory — connecting LiFePO₄ directly to a smart alternator will undercharge or damage the battery
- **Battery location options:** Under driver/passenger seat, or in the rear garage area
- **The Lynx Distributor solves the "single stud" problem:** In the Boxer, finding a single ground point for all DC negatives is difficult. The Lynx− bus acts as the single-point negative collection point, with one 50mm² cable to chassis.

## IoT Monitoring (Future)

The project includes a research document (`reserse_iot_embed.md`) for low-cost IoT monitoring:

| Priority | Device | Cost (EUR) | Benefit |
|---|---|---|---|
| 1 | ESP32 + VE.Direct cable | ~€10 | Real-time Victron monitoring (MPPT, Orion) |
| 2 | DS18B20 temperature sensors | ~€2/each | Battery cable temp, inverter temp, ambient |
| 3 | MQ-7 + MQ-2 gas sensors | ~€12 | CO + LPG safety detection |
| 4 | PZEM-004T AC monitor | ~€10 | 230V power monitoring (V, A, W, kWh) |
| 5 | OLED SSD1306 display | ~€4 | Local dashboard |

All IoT devices use **ESPHome** framework for unified integration with **Home Assistant**.

## Documents in This Repo

| File | Description |
|---|---|
| `komplexni_dokumentace.md` | Main project documentation (Czech, 8 sections) |
| `elektro_schema_boxer.html` | Interactive SVG wiring diagram with hover details + shopping links |
| `reserse_verejne_zdroje.md` | Public source research (30+ references) |
| `reserse_iot_embed.md` | IoT embedded devices research — ESPHome/ESP32 monitoring |
| `priprava_schuzka_2026-07-09.md` | Client meeting preparation checklist (Czech) |
| `jednostrankovy_summary.md` | One-page project summary (Czech) |
| `hovor_s_klientem.txt` | Phone consultation transcript (anonymized, Czech) |
| `whatsapp_konverzace.txt` | Raw WhatsApp conversation export (anonymized, Czech) |

## Wiring Diagram

Open `elektro_schema_boxer.html` in any browser for an **interactive SVG wiring diagram**. Hover over any component to see:
- What it does
- Why that specification was chosen
- Source references (Victron manuals, standards)
- Click to open e-shop links for purchase

The diagram covers the **complete system** including the minimalist phase (current) and future expansion (solar, water system, floor heating).

## References & Resources

- **Victron Van-Motorhome Manual:** [Official wiring diagrams](https://www.victronenergy.com/upload/documents/Van-Motorhome-Manual-&-Drawing-3-monitoring-setups-MultiPlus-3kVA-12V-230V-50Hz-Li-SuperPack-NG.pdf)
- **Wireframe van wiring guides:** [usewireframe.com/guides](https://usewireframe.com/guides) — DC-DC, Lynx, MultiPlus, 600Ah system
- **Wiring Unlimited:** [Victron's essential wiring guide](https://www.victronenergy.com/upload/documents/Wiring-Unlimited-EN.pdf)
- **The Van Conversion — MultiPlus wiring:** [thevanconversion.com](https://www.thevanconversion.com/post/victron-multiplus-wiring-diagram)
- **Off-Grid Benchmark — Van Electrical Guide:** [offgridbenchmark.com](https://www.offgridbenchmark.com/guides/van-life-electrical-guide/)
- **Roam Wired — Orion XS install guide:** [roamwired.com](https://roamwired.com/blog/victron-orion-xs-install)
- **TITAN Lithium — Boxer battery guide:** [titanlithium.co.uk](https://titanlithium.co.uk/de/pages/lithium-battery-peugeot-boxer)
- **WattCycle 314Ah review:** [levinguyen.com](https://levinguyen.com/blog/wattcycle-battery-review/)
- **Victron Community — Peugeot Boxer setup:** [communityarchive.victronenergy.com](https://communityarchive.victronenergy.com/questions/238790/peugeot-boxer-wiring-set-up.html)

---

*Project started: 2026-07-08 | Repository: [github.com/outpost2026/van-peugeot-offgrid](https://github.com/outpost2026/van-peugeot-offgrid)*
