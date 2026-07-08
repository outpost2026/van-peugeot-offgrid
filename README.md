<div align="left">
  <a href="https://github.com/outpost2026/van-peugeot-offgrid/blob/main/README.en.md">
    <img src="https://flagcdn.com/24x18/gb.png" alt="EN" height="18"> English
  </a>
</div>

# ⚡ Elektrifikace dodávky Peugeot Boxer 2021 — off-grid 12V/230V

**Off-grid Victron systém pro nezávislé bydlení v dodávce.** Minimalistický setup: lednice 12V, MaxxFan, USB porty, jedna 230V zásuvka, nabíjení z alternátoru + soláru (budoucnost).

---

## Architektura systému

```
Alternátor (Euro6) → Orion XS 50A ─┐
                                    ├── Lynx Distributor M10 ←── Baterie Wattcycle 314Ah
FV panel AIKO 445W → MPPT 100/50 ──┘           │
                                          ┌─────┴──────┐
                                     MultiPlus C       12V blok K735A
                                    12/1600/70-16      │──├ LED světla
                                          │            │──├ USB/12V zásuvky
                                     AC rozvaděč       │──├ Lednice 12V
                                     ├── zásuvky 230V  │──├ MaxxFan
                                     ├── podlahovka    │──├ Naftové topení
                                     └── bojler        └──├ Čerpadlo (future)
```

## Komponenty

| Komponenta | Specifikace | Role |
|---|---|---|
| **Baterie** | Wattcycle 12V 314Ah Mini LiFePO₄ (200A BMS, ~4 kWh) | Hlavní úložiště energie |
| **Měnič/nabíječ** | Victron MultiPlus C 12/1600/70-16 (1300W kont. / 3000W peak) | Srdce systému: měnič, nabíječka 70A, transfer, PowerAssist |
| **DC-DC nabíječ** | Victron Orion XS 12/12-50A (fanless, Bluetooth) | Nabíjení z alternátoru za jízdy — nutnost pro Euro6 smart alternátor |
| **Solární regulátor** | Victron SmartSolar MPPT 100/50 (Bluetooth) | Řízení solárního panelu |
| **Solární panel** | AIKO Nebular 445W lightweight (8,6 kg, Voc ~40V) | Future — momentálně není instalován |
| **DC sběrnice** | Victron Lynx Distributor M10 (1000A, 4× MEGA pojistky) | Centrální rozvod + jištění DC |
| **12V distribuce** | Blok K735A (12 cest, nožové pojistky) | Rozvod k 12V spotřebičům |

### Klíčová konstrukční rozhodnutí

- **Orion XS GND → kostra** (NE na zápornou sběrnici Lynxu, NE na startovací baterii) — dle Victron RV SYSTEM 3
- **MultiPlus zemní relé = ON** — nutné pro funkci RCD v ostrovním režimu
- **PowerAssist** — MultiPlus dokrmí chybějící ampéry z baterie při slabém kempovém přívodu
- **Vše na 230V dvoupólové** — kempová síť může mít přehozenou fázi a nulák
- **Průřez 50mm²** pro hlavní DC trunk (baterie ↔ Lynx ↔ MultiPlus) — dimenzováno na zátěž ~130–160A, max délka 0,4m
- **50mm² pro Lynx− → kostra** — jednobodové ukostření bez zemních smyček

## Kabeláž

| Okruh | Průřez | Jištění |
|---|---|---|
| Baterie ↔ Lynx / MultiPlus | 50mm² | MEGA 200A |
| Lynx− → kostra | 50mm² | — |
| MPPT ↔ Distributor | 16mm² | MEGA 60A |
| Orion XS (IN/OUT/GND) | 16mm² | MEGA 60A (obě strany) |
| 12V blok ↔ Distributor | 16mm² | MEGA 60A |
| Solár → MPPT (PV) | 6mm² | DC odpojovač C20 |
| Lednice 12V | 6mm² | nožová 15A |
| Naftové topení | 6mm² | nožová 20A |
| USB / 12V zásuvky | 2,5mm² | nožová 10A |
| Světla LED | 1,5mm² | nožová 10A |
| MaxxFan | 1,5mm² dvoulinka | nožová 5A |
| 230V zásuvky | 3×2,5mm² | MCB 16A |
| PE → kostra | 6mm² žluto-zelená | — |

## Stav projektu (červenec 2026)

| Doma ✅ | K dokoupení ❓ | Budoucnost 🔮 |
|---|---|---|
| Baterie Wattcycle 314Ah | Lynx Distributor M10 | Solární panel AIKO 445W |
| MultiPlus C 12/1600/70-16 | MEGA pojistky (2×200A, 4×60A) | Čerpadlo + boiler |
| Orion XS 12/12-50A | AC jistící prvky (RCBO, RCD, MCB) | IoT monitoring |
| Hydraulické kleště | Kabeláž (50/16/6mm²) | |
| Battery Switch 275A | Lednice, MaxxFan, světla | |
| Peugeot Boxer 2021 | VE.Bus Smart dongle | |

## Postup

1. **9. 7. 2026** — Osobní konzultace (kontrola komponent, finální odsouhlasení, podmínky)
2. **Nákup** — chybějící komponenty
3. **Realizace** — montáž Lynx Distributoru → DC část → AC část → konfigurace MultiPlus → oživení
4. **Rozšíření** — solár, IoT monitoring (ESP32 + ESPHome)

---

## Dokumentace v tomto repu

| Soubor | Popis |
|---|---|
| `komplexni_dokumentace.md` | Hlavní projektová dokumentace (8 sekcí) |
| `elektro_schema_boxer.html` | Interaktivní SVG schéma zapojení |
| `reserse_verejne_zdroje.md` | Rešerše 30+ zdrojů (Victron, Boxer, WattCycle, Orion XS) |
| `reserse_iot_embed.md` | Rešerše IoT zařízení (ESP32, ESPHome, senzory) |
| `priprava_schuzka_2026-07-09.md` | Checklist na osobní konzultaci s klientem |
| `jednostrankovy_summary.md` | Jednostránkový přehled pro klienta |

## Odkazy

- Schéma: https://systeq.cz/projekty/dodavka_kuba/elektro.html
- Konzultant: [systeq.cz](https://systeq.cz/)
- Victron van manual: [Victron Van-Motorhome Manual](https://www.victronenergy.com/upload/documents/Van-Motorhome-Manual-&-Drawing-3-monitoring-setups-MultiPlus-3kVA-12V-230V-50Hz-Li-SuperPack-NG.pdf)
- Wireframe guides: [usewireframe.com/guides](https://usewireframe.com/guides)
- Wiring Unlimited: [Victron Wiring Unlimited](https://www.victronenergy.com/upload/documents/Wiring-Unlimited-EN.pdf)
