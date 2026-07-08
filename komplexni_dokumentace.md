# Projekt elektrifikace dodávky — Peugeot Boxer 2021

**Klient:** Kuba Sládek  
**Konzultant:** Ondřej Soušek (Systeq.cz)  
**Datum:** 2026-07-08  
**Stav:** Příprava, konzultace, částečná realizace


## 1. Přehled projektu

**Elektrifikace dodávky Peugeot Boxer 2021 **pro obytné účely — **off-grid 12V/230V systém** postavený na komponentech Victron Energy. Cílem je vytvořit funkční a bezpečnou elektroinstalaci umožňující nezávislé bydlení v dodávce (vaření, svícení, chlazení, vytápění, nabíjení zařízení).


## 2. Komponenty — analýza HTML schématu

### 2.1 Zdroje a jádro systému

| Komponenta | Specifikace | Stav |
| - | - | - |
| **Baterie** | Wattcycle 12V 314Ah Mini LiFePO4 (~4 kWh, využit. ~3,2 kWh; BMS 200A) |  |
| **MultiPlus C** | Victron 12/1600/70-16 (měnič 1300W/špička 3000W + nabíječ 70A + transfer + zemní relé) |  |
| **Solární panel** | AIKO Nebular 445W lightweight (Voc ~40V, Isc ~14A, 8,6 kg) |  |
| **MPPT** | Victron SmartSolar 100/50 (Bluetooth, max 50A, max vstup 100V) |  |
| **Orion XS** | Victron 12/12-50A DC-DC nabíječ z alternátoru (50A, detekce běhu motoru) |  |
| **Alternátor** | Peugeot Boxer 2021 Euro6 (smart) |  |


### 2.2 Distribuce a jištění DC

| Komponenta | Specifikace | Stav |
| - | - | - |
| **Lynx Distributor M10** | Centrální DC sběrnice 1000A, 4 jištěné pozice MEGA |  |
| **MEGA 200A (×2)** | Hlavní pojistka baterie + větev měniče |  |
| **MEGA 60A (×4)** | Jištění MPPT, Orion IN/OUT, 12V blok |  |
| **Battery Switch 275A** | Hlavní ruční odpojovač |  |
| **12V blok K735A** | 12-cestný distribuční blok s LED a nožovými pojistkami |  |


### 2.3 AC rozvody (230V)

| Komponenta | Specifikace | Stav |
| - | - | - |
| **RCBO 2P 16A/30mA typ A** | Jistič + chránič vstupu z kempu |  |
| **RCD 2P 30mA typ A** | Hlavní chránič AC-OUT (zásuvky/podlahovka/bojler) |  |
| **MCB 2P 16A** | Jistič zásuvkového okruhu |  |
| **MCB 2P 10A** | Jistič podlahového topení |  |
| **MCB 2P 16A** | Jistič bojleru |  |
| **PE sběrnice** | Sběrný bod ochranného vodiče → kostra 6mm² |  |
| **Kemp 230V (CEE)** | Přípojka kempové sítě |  |


### 2.4 Spotřebiče 12V

| Komponenta | Specifikace | Stav |
| - | - | - |
| **LED světla** | Vnitřní osvětlení, 1,5mm², poj. 10A |  |
| **USB / 12V zásuvky** | Nabíjecí porty, 2,5mm², poj. 10A |  |
| **Lednice 12V** | Kompresorová (Indel B apod.), 6mm², poj. 15A |  |
| **MaxxFan** | Střešní větrák 12V, 1,5mm², poj. 5A |  |
| **Naftové topení 5kW** | LF Bros / Planar, 6mm², poj. 20A |  |
| **Čerpadlo 12V + relé** | Shurflo/Seaflo, 2,5mm², poj. 10A |  |
| **Kohoutky (mikrospínač)** | Reich/Comet — signál pro relé čerpadla |  |
| **Podlahové topení 230V** | Rohož ~320W, 3×1,5mm², vlastní MCB |  |
| **Bojler plyn/elektro** | 230V těleso ≤1000W (jen na kempu) |  |
| **Zásuvky 230V** | Schuko za chráničem |  |


### 2.5 Doplňky

| Komponenta | Specifikace | Stav |
| - | - | - |
| **CO + LPG detektor** | Bezpečnost (CO k lůžku, LPG nízko) |  |
| **VE.Bus Smart dongle** | Bluetooth rozhraní pro MultiPlus (MultiPlus C nemá BT) |  |
| **Hydraulické kleště** | Na krimpování kabelových ok |  |


### 2.6 Kabeláž (průřezy)

| Okruh | Průřez | Poznámka |
| - | - | - |
| Baterie ↔ Lynx / MultiPlus | **50mm²** | Hlavní trunk, max 0,4m |
| Lynx− → kostra | **50mm²** | Jednobodové ukostření |
| MPPT ↔ Distributor | **16mm²** | MEGA 60A |
| Orion XS (IN/OUT/GND) | **16mm²** | 60A; GND → kostra |
| 12V blok ↔ Distributor | **16mm²** | MEGA 60A |
| Solár panel → MPPT (PV) | **6mm²** | MC4, max 5m/pól |
| Světla LED | **1,5mm²** | Poj. 10A, max 3m |
| USB / 12V zásuvky | **2,5mm²** | Poj. 10A, max 3m |
| Lednice | **6mm²** | Poj. 15A, max 3m |
| Čerpadlo | **2,5mm²** | Poj. 10A, max 3m |
| Naftové topení | **6mm²** | Poj. 20A, max 3m |
| MaxxFan | **1,5mm² dvoulinka** | Poj. 5A, max 4m |
| AC-IN / zásuvky | **3×2,5mm²** | 16A |
| Podlahovka | **3×1,5mm²** | Vlastní okruh |
| PE → kostra | **6mm²** | Žluto-zelená |




## 3. Telefonická konverzace

### Klíčové body:

1. **Prvotní kontakt** — Kuba oslovil Ondru s žádostí o pomoc s elektroinstalací dodávky. Má vše vymyšlené, ale nechce se pouštět do zapojování sám.

2. **Místo realizace** — Kuba může dojet do Draháně, ale dodávka je velká a těžko manévrovatelná. Nakonec se domlouvají na konzultaci s komponentami.

3. **Komponenty** — Kuba má 314Ah LiFePO4 baterii, Victron komponenty. MPPT regulátor má, FV zatím ne.

4. **Servis a přenastavení** — MultiPlus se musí přenastavit na LiFePO4 profil přes příslušný modul.

5. **Časový rámec** — Kuba pracuje z domu, má čas. Může dorazit o víkendu nebo následující týden. Bude upřesněno.

6. **Know-how a byznys** — Ondra (konzultant) má IČO, rozjíždí vlastní projekty. Ondra má v elektroinstalacích dlouholeté zkušenosti.

7. **Podklady** — Kuba již poslal základní podklady (HTML diagram, seznam komponent) přes WhatsApp; další budou upřesněny osobně.

8. **Reference** — Kuba zmiňuje možnost použít projekt jako referenci pro dodávkářskou komunitu.


## 4. Diskuze

### Klíčové body:

1. **Diagram** — Kuba poslal HTML diagram. Kuba si není jistý, zda je diagram zcela přesný. Odborník jej pouze viděl a prozatím zhodnotil jako OK

2. **Minimalistický požadavek** — Kuba chce **minimalisticky**: jen větrák, lednici, USB, jednu 230V zásuvku. Žádné čerpadlo, boiler, podlahovka atd. — ty nemá a zatím nepotřebuje.

3. **Stav komponent:**

   - ✅ **Doma:** Baterie Wattcycle, Orion XS, hydraulické kleště, switch 275A, MultiPlus C 12/1600/70-16

   - ❌ **Koupit: (bude upřesněno během osobní konzultace)  
**Solární panel AIKO, Lynx Distributor, pojistkové skříně, AC prvky (RCD, MCB), 12V spotřebiče (lednice, větrák, světla), VE.Bus dongle

   - ❌ **Nemá:** FV panel není na střeše, pojistková skříň není koupená

4. **MultiPlus jako klíčový prvek** — Kuba zdůrazňuje, že MultiPlus zjednodušuje zapojení (není jen měnič, ale i nabíječka, přepínač sítě, power assist). Kuba má pro něj konfigurační modul (VE.Bus).

5. **Otázka kabeláže** — rozhodneme společně

6. **Setkání** — Domluva na osobní schůzku: Kuba doveze komponenty k Ondrovi na chatu, proberou projekt, domluví podmínky.

7. **Bezpečnost a soukromí** — Kuba nechtěl zveřejňovat jméno a telefon. = jméno a tel. číslo klienta je odstraněno.

8. **Ondrova role** — Ondra nemá přímou zkušenost s Victronem.  Nutno prozkoumat architekturu a vytvořit projekt.

9. **Ostatní** — Kuba je v Bakově nad Jizerou



## 5. Stav projektu — inventura

### Co je k dispozici (fyzicky doma — stav k 08.07.2026):

- Baterie Wattcycle 12V 314Ah LiFePO4

- Orion XS 12/12-50A DC-DC nabíječ

- MultiPlus C 12/1600/70-16

- Hydraulické kleště

- Dodávka Peugeot Boxer 2021

*Pozn.: Stav ostatních komponent bude upřesněn při osobní konzultaci.*

### Co je potřeba dokoupit:

- **Lynx Distributor M10** — centrální DC sběrnice

- **MEGA 200A (×2)** — hlavní pojistky

- **AC prvky:** RCBO 2P, RCD 2P 30mA typ A, MCB 2P 16A/10A

- **12V spotřebiče:** Lednice, MaxxFan, světla, USB porty, naftové topení

- **Kabeláž:** 50mm², 16mm², 6mm², 2,5mm², 1,5mm² dle tabulky

- **PE sběrnice + bezpečnost:** CO + LPG detektor

- **VE.Bus Smart dongle** (doporučeno)

### Co je na voze (stávající):

- Alternátor Euro6 (smart)

- Startovací baterie

- Kabina, prostor pro vestavbu


## 6. Požadavky klienta (minimalistický setup)

Kuba aktuálně požaduje pouze:

1. **Lednici 12V** — kompresorová, zapojená přes autozásuvku/12V okruh

2. **Vestavěný větrák (MaxxFan)** — vlastní okruh s pojistkou

3. **12V USB porty** — nabíjení zařízení

4. **Jedna 230V zásuvka** — pro občasné spotřebiče (přes MultiPlus)

5. **Možnost nabíjení:** z alternátoru (Orion XS) + soláru (do budoucna)

6. **Možnost připojení kempu 230V** pro nabíjení baterie a přímé napájení

**Nepotřebuje (zatím):**

- Čerpadlo a vodní systém

- Bojler na 230V

- Podlahové topení

- CO/LPG detektor (doporučeno ale řešit)

- Naftové topení (řeší samostatně)


## 7. Návrh dalšího postupu

### Fáze 1: Osobní konzultace (plánováno na 9. 7. 2026)

- Kuba doveze komponenty k Ondrovi

- Prohlídka fyzického stavu, odsouhlasení kompatibility

- Definice finálního minimalistického zapojení

- Cenová kalkulace a odměna pro konzultanta

- Časový harmonogram

### Fáze 2: Nákup chybějících komponent

- Lynx Distributor + pojistky MEGA

- AC jistící prvky (RCBO, RCD, MCB)

- 12V spotřebiče dle odsouhlaseného rozsahu

- Kabeláž dle tabulky průřezů

### Fáze 3: Realizace

- Montáž Lynx Distributoru

- Zapojení DC části (baterie → Lynx → MultiPlus → 12V blok)

- Zapojení AC části (MultiPlus → RCD → MCB → zásuvky)

- Konfigurace MultiPlus přes VE.Bus (LiFePO4 profil, zemní relé ON, input limit)

- Zapojení Orion XS (GND → kostra dle Victron RV SYSTEM 3)

- Oživení a testování

### Fáze 4: Rozšíření (budoucnost)

- Instalace solárního panelu + MPPT

- Přidání čerpadla, boileru, topení

- Plnohodnotný AC rozvod

### Technické poznámky:

- **Orion XS GND → kostra** (NE na Lynx−) dle Victron RV SYSTEM 3

- **Vše na 230V dvoupólové** (kemp může mít přehozenou polaritu)

- **Zemní relé MultiPlusu ON** ve VEConfigure

- **Power assist** — MultiPlus dokrmí chybějící ampéry z baterie při omezeném kempovém proudu

- **BMS 200A = strop systému** — jen jeden velký 230V spotřebič v čase

- **Průřez 50mm²** dimenzován na zátěž (130–160A), ne na délku (trasa ~20–40 cm)


## 8. Zdroje

- Schéma zapojení: `elektro\_kuba\_sladek.html` (lokálně) / [https://systeq.cz/projekty/dodavka\_kuba/elektro.html](https://systeq.cz/projekty/dodavka_kuba/elektro.html)

- Web konzultanta: [https://systeq.cz](https://systeq.cz/)

