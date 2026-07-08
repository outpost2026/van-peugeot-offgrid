# Příprava na schůzku s klientem — 9. 7. 2026

**Klient:** —anonymizováno—  
**Místo:** Konzultace u konzultanta  
**Účel:** Osobní konzultace — kontrola komponent, odsouhlasení zapojení, domluva podmínek

---

## 1. Checklist — fyzická kontrola komponent (klient přiveze)

| Komponenta | Stav (OK/poškozeno/chybí) | Poznámka |
|---|---|---|
| **Baterie Wattcycle 314Ah** | | Zkontrolovat: fyzický stav, terminály, BMS (Bluetooth?), svorkovnice |
| **MultiPlus C 12/1600/70-16** | | Zkontrolovat: sériové číslo, firmware, VE.Bus port, terminály |
| **Orion XS 12/12-50A** | | Zkontrolovat: konektory, propojovací kabel, REMOTE kabel |
| **Battery Switch 275A** | | Zkontrolovat typ (1-pól / 2-pól) |
| **Hydraulické kleště** | | Jaké okuje? Potřeba koupit okuje? |
| **Kabeláž (pokud má)** | | Jaké průřezy a délky už má doma? |
| **VE.Bus Smart dongle** | | Má ho, nebo teprve koupí? |
| **Ostatní:** | | Co ještě klient přiveze? |

---

## 2. Otázky na klienta

### 2.1 Rozsah projektu (minimalistický setup)

- [ ] **Lednice 12V** — jakou má/model? Rozměry, příkon (A/h)?
- [ ] **MaxxFan** — jaký model? (6xxx s remote?)
- [ ] **Světla** — jaká? LED pásky, bodovky? Kolik okruhů?
- [ ] **USB/12V zásuvky** — kolik? Kde?
- [ ] **230V zásuvka** — jen jedna? Kam umístit?
- [ ] **FV panel AIKO 445W** — koupí teď nebo až později?
- [ ] **MPPT 100/50** — už ho má doma? V krabici?

### 2.2 Nákupní seznam (odsouhlasit)

- [ ] Lynx Distributor M10 — objednat?
- [ ] MEGA pojistky (2×200A, 4×60A) — objednat?
- [ ] AC prvky: RCBO 2P 16A/30mA, RCD 2P 30mA typ A, MCB 2P 16A
- [ ] PE sběrnice + DIN lišta pro AC rozvaděč
- [ ] Kabeláž: 50mm² (2m černá + 2m červená), 16mm², 6mm² atd.
- [ ] 12V blok K735A (nebo jiný)?
- [ ] CO/LPG detektor — řešit teď nebo později?
- [ ] VE.Bus Smart dongle — je potřeba (pokud MultiPlus C nemá BT)?

### 2.3 Instalace a umístění

- [ ] Kde bude **Lynx Distributor** umístěn? (pod sedadlem? v garáži?)
- [ ] Kde bude **MultiPlus**? (ventilace! horký vzduch)
- [ ] Kde bude **baterie**? (co nejblíže Lynxu, max 40cm propoj 50mm²)
- [ ] Kde bude **AC rozvaděč**? (RCD, MCB, PE sběrnice)
- [ ] Průchod kabeláže — kudy povedou kabely? (kabelové kanály?)
- [ ] **Kostřící bod** — kde je v Boxeru vhodné místo pro jednobodové ukostření?

### 2.4 Podmínky spolupráce

- [ ] **Cenová kalkulace** — odměna konzultantovi? Paušál / hodinovka?
- [ ] **Harmonogram** — kdy je reálné začít? (víkendy? celé dny?)
- [ ] **Místo realizace** — u konzultanta? Nebo u klienta?
- [ ] **Reference** — Klient zmínil možnost použití jako reference pro komunitu — jakou formou?

---

## 3. Technické body k prodiskutování

### 3.1 Schéma zapojení — odsouhlasit finální verzi

- [ ] Ukázat aktuální schéma (HTML / diagram)
- [ ] Odsouhlasit: **Orion XS GND → kostra** (NE startovací baterie)
- [ ] Odsouhlasit: **Zemní relé MultiPlus = ON** (VEConfigure)
- [ ] Odsouhlasit: **MultiPlus LiFePO4 profil** — nutné nahrát přes VE.Bus
- [ ] Odsouhlasit: **PowerAssist** — zapnout, limit kempu 6A/10A/16A?
- [ ] Odsouhlasit: **Schéma zapojení 12V bloku** — co na který okruh?

### 3.2 Důležité technické detaily

- **MultiPlus C nemá Bluetooth** — nutný VE.Bus Smart dongle pro konfiguraci i monitoring
- **WattCycle BMS 200A** — strop je 2400W; MultiPlus 12/1600 (1300W kontinuální + 3000W peak) je v bezpečí
- **Průřez 50mm²** mezi baterií a Lynxem — max délka 40cm
- **Smart alternátor Boxeru** = povinný DC-DC nabíječ (Orion XS)
- **Solární příprava** — natáhnout PV kabely 6mm² ke střeše už teď (i když FV panel není)

### 3.3 Bezpečnost

- [ ] Hlavní vypínač baterie (Battery Switch 275A) — kam umístit? (dostupný, označený)
- [ ] Všechny DC kabely jištěny u zdroje (MEGA pojistky v Lynxu)
- [ ] AC dvoupólově jištěno (přepólovaný kemp)
- [ ] Větrání prostoru MultiPlus

---

## 4. Materiály vzít na schůzku

- [ ] Vytištěné schéma / tablet s diagramem
- [ ] Tento checklist
- [ ] Jednostránkový summary projektu (pro Kubu)
- [ ] Kalkulačka / cenový rozpis
- [ ] Poznámkový blok

---

## 5. Akční body po schůzce

- [ ] Zapsat stavy komponent do `komplexni_dokumentace.md`
- [ ] Aktualizovat nákupní seznam
- [ ] Potvrdit harmonogram
- [ ] Commitnout + pushnout změny do GitHubu
