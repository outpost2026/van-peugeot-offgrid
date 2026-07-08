# Rešerše veřejných zdrojů — off-grid elektrifikace dodávek (Victron + LFP + FV)

## 1. Oficiální dokumentace Victron

### 1.1 Schémata pro dodávky a obytná vozidla
- **US Van Manual & Drawing VEBus BMS V2 MultiPlus-II 3kVA** — oficiální schéma Victron pro 12V systém s Lynx Distributorem, BMS, MPPT, Orion XS. Klíčový referenční dokument: https://www.victronenergy.com/upload/documents/US-Van-Manual-&-Drawing-VEBus-BMS-V2-MultiPlus-II-3kVA-12V-120V-60Hz.pdf
- **Van-Motorhome Manual & Drawing 3 monitoring setups** — 3 varianty zapojení s MultiPlus 3kVA: https://www.victronenergy.com/upload/documents/Van-Motorhome-Manual-&-Drawing-3-monitoring-setups-MultiPlus-3kVA-12V-230V-50Hz-Li-SuperPack-NG.pdf
- **Lynx Distributor Manual** (rev 04/2025): https://www.victronenergy.com/upload/documents/Lynx_Distributor/24531-Lynx_Distributor_Manual-pdf-en.pdf

### 1.2 Wiring Unlimited
Victron oficiální příručka "Wiring Unlimited" — základní reference pro dimenzování kabelů, pojistek, uzemnění (vícekrát citováno v HTML schématu projektu).

---

## 2. Nástroje pro návrh zapojení

### 2.1 Wireframe (usewireframe.com)
Profesionální online nástroj pro tvorbu schémat zapojení dodávek. Obsahuje template pro:
- **600Ah Victron systém s 3000W MultiPlus & Lynx** — detailní návod: https://usewireframe.com/guides/600ah-victron-campervan-wiring-diagram-3000w-lynx
- **Lynx Distributor wiring** — https://usewireframe.com/guides/van-victron-lynx-distributor-wiring-diagram
- **Lynx Smart BMS wiring** — https://usewireframe.com/guides/van-victron-lynx-smart-bms-wiring-diagram
- **DC-DC Orion XS wiring** — https://usewireframe.com/guides/van-dcdc-charger-wiring-diagram
- **MultiPlus/Inverter wiring** — https://usewireframe.com/guides/van-inverter-wiring-diagram

### 2.2 Wireframe — klíčové poznatky pro projekt
- 3000W MultiPlus 12/3000/120 při 270A vyžaduje **duální 50mm² kabel na terminál** (M8 terminál neumožňuje 95mm²)
- Lynx Distributor acceptuje MEGA pojistky v 4 pozicích, používá RJ10 kabel pro propojení s Lynx Smart BMS
- Orion XS 50A: 16mm² kabel, MEGA 60-70A pojistka na vstupu i výstupu
- 600Ah systém potřebuje **400A Class T pojistku** (ne ANL) kvůli vysokému zkratovému proudu lithiové baterie

---

## 3. Průvodci stavbou (build guides)

### 3.1 The Van Conversion — MultiPlus Wiring Diagram
https://www.thevanconversion.com/post/victron-multiplus-wiring-diagram (2026)
- Krok za krokem: AC-IN z kempu → jistič → RCD → MCB → MultiPlus → AC-OUT → RCD → MCB → zásuvky
- Uzemnění: AC chassis ground point, DC ground point (min 5cm od sebe)
- Dimenzování kabelů a pojistek

### 3.2 Custom Solutions UK — Complete Victron Off-Grid Campervan System
https://www.customsolutionsuk.co.uk/blogs/van-life-custom-builds-motorhomes-camper-vans/complete-victron-off-grid-campervan-electrical-system-expandable (2025)
- Modulární systém: 100Ah LiFePO₄ → MPPT 100/30 → Orion 30A → IP22 nabíječka
- Možnost rozšíření: více baterií paralelně, větší invertor

### 3.3 Off-Grid Benchmark — Van Life Electrical System Guide
https://www.offgridbenchmark.com/guides/van-life-electrical-guide/ (2026)
- Kompletní průvodce od nuly: dimenzování baterie, soláru, DC-DC, měniče
- Doporučení: 200Ah LiFePO₄ = sweet spot, 200-400W solár, 30A DC-DC
- Fázování: "každý kladný vodič musí být jištěn do 12 palců (30 cm) od baterie"

### 3.4 The Vansmith — Victron MultiPlus Review & Install Tips
https://thevansmith.com/blogs/van-service-upgrades/victron-multiplus (2026)
- PowerAssist: MultiPlus dokrmí chybějící ampéry z baterie při slabém kempovém přívodu
- 3000VA MultiPlus = 2400W continuous, zvládne indukci, klimatizaci
- Ventilace: 4" clearance nad i pod jednotkou, vertikální montáž

### 3.5 Roam Wired — Victron MultiPlus for Campervans
https://roamwired.com/blog/victron-multiplus-campervan (2025)
- MultiPlus C 12/1600 = stejný model jako v projektu Kuby. Závěr: vhodný pro menší až střední systémy, 1300W continuous.

---

## 4. Specifické zdroje pro Peugeot Boxer

### 4.1 Victron Community — Peugeot Boxer Wiring Set Up
https://communityarchive.victronenergy.com/questions/238790/peugeot-boxer-wiring-set-up.html (2023)
- Boxer 2020, konverze, 200Ah LiFePO₄, solár
- Doporučení: MultiPlus 12/2000/80 pro 1600W continuous
- **LiFePO₄ = 0.5C** -> 1600W invertor vyžaduje min 320Ah baterii (potvrzuje volbu 314Ah v projektu)

### 4.2 TITAN Lithium — Battery Guide for Peugeot Boxer
https://titanlithium.co.uk/de/pages/lithium-battery-peugeot-boxer
- **Klíčové pro Boxer Euro6**: chytrý alternátor s proměnným napětím — nelze spolehlivě nabíjet LiFePO₄ bez DC-DC nabíječe (Orion XS)
- Umístění baterie: pod sedadlem řidiče/spolujezdce nebo v zadním boxu

### 4.3 Van Junkies — Full Electrical Off-Grid Kit pro Sprinter/Crafter/Boxer
https://vanjunkies.co.uk/products/sprinter-crafter-boxer-full-electrical-off-grid-camper-conversion-kit-with-monitoring (2024)
- Komerční kit: 300Ah Fogstar + 3kW MultiPlus-II + Orion XS 50A + Cerbo GX + Lynx Distributor
- Reference: stejná architektura jako projekt Kuby

### 4.4 Quirky Campers — Peugeot Boxer off-grid inzeráty
- **Boxer s Victron EasySolar 12/1600/70**: 540W solár, 200Ah LiFePO₄ (ekvivalent 400Ah AGM), Orion 30A, GX Touch 50 — https://www.quirkycampers.com/uk/for-sale/new-unique-luxury-conversion-off-grid-540w-solar-200ah-lithium-battery-peugeot-boxer-l4h2/
- **High spec Boxer**: Victron Lynx, Orion, MPPT 100/20, MultiPlus 12/1600/70, Fogstar 230Ah — identická sestava s projektem

---

## 5. WattCycle 314Ah — recenze a reálné zkušenosti

### 5.1 DIYSolarForum — WattCycle 314Ah s Victron MultiPlus
https://diysolarforum.com/threads/will-my-wattcycle-12v-314ah-battery-run-a-3000va-inverter.106499/ (2025)
- **BMS 200A = strop 2400W** při 12V. MultiPlus C 12/1600 (1300W kont.) je v bezpečí.
- MultiPlus-II 3000VA může vyžadovat paralelní 2× 314Ah pro plný výkon

### 5.2 Levi Nguyen — WattCycle Battery Review 2026
https://levinguyen.com/blog/wattcycle-battery-review/
- **Grade-A EV cells**, hliníková kostra pro odolnost vibracím (důležité v dodávce)
- 200A BMS continuous, Bluetooth monitoring
- **Poměr cena/výkon** nejlepší ve své třídě

### 5.3 AdventureTaco — 3 měsíční review Lithiového systému
https://adventuretaco.com/lithium-lifepo4-house-electrical-3-month-review/ (2025)
- WattCycle 280Ah (nyní 314Ah) + Victron SmartShunt + Orion XS + MPPT
- **LiFePO₄ gamechanger**: oproti AGM lze používat několik dní bez nabíjení
- Victron Connect = jeden app pro všechna zařízení (Shunt, Orion, MPPT)

### 5.4 WattCycle user review — RV instalace
https://www.wattcycle.com/blogs/news/replacing-100ah-dragonfly-lithium-batteries-with-wattcycle-314ah-battery
- Reálná instalace 2× 314Ah (628Ah) v RV s Victron shuntem a Orion XS 50A
- Atmos klimatizace běžela 14h na baterii (63% zbylo)
- Orion XS 50A dává ~50A při volnoběhu i jízdě

---

## 6. Orion XS — instalace a konfigurace

### 6.1 Roam Wired — Orion XS Complete Install Guide
https://roamwired.com/blog/victron-orion-xs-install (2025)
- **D+ není vyžadován** — Orion XS detekuje běh motoru z napětí (smart alternátor kompatibilní)
- Kabeláž: 16mm² pro 50A při běhu do 5m
- Pojistky: MEGA 60-70A na vstupu i výstupu
- Montáž: jakákoliv orientace (fanless), blízko baterie

### 6.2 Wireframe — Orion XS wiring bez D+
https://usewireframe.com/guides/van-dcdc-charger-wiring-diagram
- 3 konfigurace: bez D+, s D+, Orion-TR starší model
- Detailní specifikace kabelů a pojistek

### 6.3 EXPLORIST.life — Dual Orion XS instalace (YouTube)
https://www.youtube.com/watch?v=MOtXT7Ld5xs (2024)
- Náhrada Orion-TR 30A za Orion XS 50A
- Praktická ukázka kabeláže, krimpování, montáže

### 6.4 Ford Transit Forum — Dual Orion XS uzemnění
https://www.fordtransitusaforum.com/threads/dual-orion-xs-wiring-connection.104451/ (2025)
- Orion XS negativ jde na Lynx Distributor − (NE na startovací baterii)
- Zásadní: Orion XS je **non-isolated** — zemnící vodič vede minimum proudu (~2A)
- U projektu Kuby: GND → kostra dle Victron RV SYSTEM 3 — **v souladu s praxí**

---

## 7. Lynx Distributor — detailní informace

### 7.1 Uživatelská zkušenost (Ford Transit Forum)
https://www.fordtransitusaforum.com/threads/please-review-my-electrical-system-detailed-diagram-included.100112/ (2024)
- Lynx Distributor odstraňuje redundantní pojistky (stačí MEGA v Distributoru)
- Orion XS: vstup i výstup jsou jištěny v Lynx Distributoru
- **MultiPlus 2000W**: doporučeno duální 50mm² kvůli M8 terminálu

### 7.2 Evans Outdoor Adventures — All Victron RV Electrical Part 4
https://www.evansoutdooradventures.com/all-victron-rv-electrical-part-4-wiring-and-configuration/
- Reálná instalace: Lynx Distributor + MultiPlus + 2× Orion XS 1400 + Cerbo GX
- Spreadsheet-based wiring procedure
- DVCC (Distributed Voltage and Current Control) pro řízení více zdrojů nabíjení

---

## 8. Závěr a relevance pro projekt Kuby

| Oblast | Nález | Dopad na projekt |
|---|---|---|
| **Architektura** | Lynx Distributor + MultiPlus + Orion XS je standardní a osvědčená sestava | Projekt je v souladu s best practices |
| **MultiPlus C 12/1600** | Vhodný pro menší systémy do 1300W; BMS 200A je dostatečná | OK, žádná změna |
| **WattCycle 314Ah** | Grade-A články, 200A BMS, dobré recenze; Bluetooth app má výhrady | Doporučit samostatný Victron SmartShunt |
| **Orion XS GND** | GND → kostra (ne startovací baterie) = korektní zapojení | Potvrzuje správnost návrhu |
| **Kabeláž 50mm²** | Victron specifikuje 50mm² pro MultiPlus C 12/1600 (M8 terminál) | Korektní |
| **Peugeot Boxer Euro6** | Vyžaduje DC-DC nabíječ (Orion XS) kvůli smart alternátoru | Orion XS je nutnost; má ho |
| **PowerAssist** | Umožňuje dokrmit slabý kempový proud z baterie | Klíčová funkce pro Kubu |

---

## 9. Zdroje (linky)

- Wireframe (návrh schémat): https://usewireframe.com/guides
- Victron Van Manual: https://www.victronenergy.com/upload/documents/US-Van-Manual-&-Drawing-VEBus-BMS-V2-MultiPlus-II-3kVA-12V-120V-60Hz.pdf
- The Van Conversion: https://www.thevanconversion.com/post/victron-multiplus-wiring-diagram
- Custom Solutions UK: https://www.customsolutionsuk.co.uk/blogs/van-life-custom-builds-motorhomes-camper-vans/complete-victron-off-grid-campervan-electrical-system-expandable
- Off-Grid Benchmark: https://www.offgridbenchmark.com/guides/van-life-electrical-guide/
- The Vansmith: https://thevansmith.com/blogs/van-service-upgrades/victron-multiplus
- Roam Wired MultiPlus: https://roamwired.com/blog/victron-multiplus-campervan
- Roam Wired Orion XS: https://roamwired.com/blog/victron-orion-xs-install
- Victron Community Boxer: https://communityarchive.victronenergy.com/questions/238790/peugeot-boxer-wiring-set-up.html
- TITAN Lithium Boxer: https://titanlithium.co.uk/de/pages/lithium-battery-peugeot-boxer
- Van Junkies: https://vanjunkies.co.uk/products/sprinter-crafter-boxer-full-electrical-off-grid-camper-conversion-kit-with-monitoring
- WattCycle recenze: https://levinguyen.com/blog/wattcycle-battery-review/
- AdventureTaco: https://adventuretaco.com/lithium-lifepo4-house-electrical-3-month-review/
- Ford Transit Forum Lynx/Orion: https://www.fordtransitusaforum.com/threads/please-review-my-electrical-system-detailed-diagram-included.100112/
- Evans Outdoor Adventures: https://www.evansoutdooradventures.com/all-victron-rv-electrical-part-4-wiring-and-configuration/
- Quirky Campers Boxer: https://www.quirkycampers.com/uk/for-sale/new-unique-luxury-conversion-off-grid-540w-solar-200ah-lithium-battery-peugeot-boxer-l4h2/

---

*Dokument generated 2026-07-08*
