# Projekt elektrifikace — Peugeot Boxer 2021

**Klient:** Kuba Sládek | **Konzultant:** Ondřej Soušek (systeq.cz)

---

## Cíl
Off-grid 12V/230V systém pro nezávislé bydlení v dodávce — minimalistický setup:
lednice, větrák, USB porty, jedna 230V zásuvka, nabíjení z alternátoru + soláru.

---

## Jádro systému

| Komponenta | Role |
|---|---|
| **Wattcycle 314Ah LiFePO4** | Hlavní baterie ~4 kWh (využit. ~3,2 kWh) |
| **Victron MultiPlus C 12/1600/70-16** | Měnič 1300W + nabíječ 70A + power assist + transfer |
| **Victron Orion XS 12/12-50A** | DC-DC nabíječ z alternátoru (smart alternátor!) |
| **Victron SmartSolar MPPT 100/50** | Solární regulátor (panel AIKO 445W — future) |
| **Lynx Distributor M10** | Centrální DC sběrnice + 4× MEGA pojistka |

---

## Architektura zapojení

```
Alternátor → Orion XS → Lynz Dist. ← Wattcycle 314Ah
                                ↓
                          MultiPlus C ← MPPT ← AIKO 445W
                              ↓
                          AC rozvaděč (RCD → MCB → zásuvka)
                              ↓
                          12V blok → lednice, MaxxFan, USB světla
```

- **Orion XS GND → kostra** (NE startovací baterie)
- **MultiPlus zemní relé = ON**
- **PowerAssist** — dokrmí slabý kemp ze soláru/baterie
- **Vše na 230V dvoupólové** (kemp může mít přehozenou polaritu)

---

## Stav (červenec 2026)

| **Doma ✅** | **Dokoupit ❓** | **Future 🔮** |
|---|---|---|
| Baterie Wattcycle 314Ah | Lynx Distributor + pojistky | Solární panel AIKO 445W |
| MultiPlus C 12/1600/70-16 | AC jistící prvky (RCD, MCB) | Čerpadlo, boiler, topení |
| Orion XS 12/12-50A | Kabeláž 50/16/6mm² | IoT monitoring |
| Hydraulické kleště | Lednice, MaxxFan, světla | |
| Battery Switch 275A | VE.Bus Smart dongle | |
| Dodávka Peugeot Boxer 2021 | | |

---

## Další postup

1. **9. 7. 2026** → Osobní konzultace (kontrola komponent, finální odsouhlasení)
2. **Nákup** → Lynx, pojistky, kabeláž, AC prvky
3. **Realizace** → Montáž, zapojení, oživení
4. **Rozšíření** → Solár, IoT monitoring
