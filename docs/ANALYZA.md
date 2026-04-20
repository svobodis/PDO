# Analýza projektu a specifikace požadavků

Tento dokument definuje cíle projektu, charakteristiku uživatelů a technické požadavky na Turnajový systém. Analýza slouží jako podklad pro návrh architektury a následnou implementaci.

## 1. Cíle projektu
Hlavním cílem je vytvořit platformu pro správu amatérských sportovních turnajů, která eliminuje administrativní zátěž organizátora spojenou s tvorbou harmonogramů a distribucí výsledků. Systém klade důraz na nulovou bariéru vstupu (není vyžadována registrace) a okamžitou odezvu.

## 2. Analýza aktérů (Stakeholders)

### 2.1 Organizátor (Administrátor)
Uživatel zodpovědný za založení turnaje a jeho průběh.
- Kontext: Často se nachází v terénu, používá mobilní zařízení, pracuje pod časovým tlakem.
- Potřeby: Rychlé zadávání dat, automatické generování rozpisů, export tiskových podkladů.

### 2.2 Divák (Veřejný uživatel)
Pasivní uživatel sledující průběh události.
- Kontext: Sleduje výsledky na vlastním zařízení (BYOD - Bring Your Own Device).
- Potřeby: Okamžitý přístup k aktuálnímu skóre a tabulkám bez nutnosti interakce.

## 3. Funkční požadavky (FR)
- FR-01: Systém umožní vytvořit turnaj pro sporty Fotbal a Házená.
- FR-02: Podpora herních systémů: Každý s každým, Skupinový, Vyřazovací pavouk a Kombinovaný systém.
- FR-03: Automatické generování bezkolizního harmonogramu zápasů na základě počtu hřišť.
- FR-04: Živý zápis výsledků s okamžitou synchronizací do diváckého pohledu.
- FR-05: Správa týmů včetně nahrávání grafických logotypů.
- FR-06: Export účastnických diplomů ve formátu PDF.

## 4. Nefunkční požadavky (NFR)
- NFR-01: Dostupnost: Webové rozhraní musí být plně responzivní (Mobile-First).
- NFR-02: Bezpečnost: Modifikace dat je povolena pouze držiteli unikátního administrátorského tokenu.
- NFR-03: Výkon: Aktualizace diváckého pohledu musí probíhat v intervalu maximálně 5 sekund.
- NFR-04: Perzistence: Systém musí uchovávat historii nedávno navštívených turnajů v lokálním úložišti prohlížeče.

## 5. Uživatelské scénáře (User Stories)
- Jako organizátor chci přidat 10 týmů a nechat je náhodně rozlosovat do dvou skupin, abych ušetřil čas s přípravou.
- Jako divák chci na svém telefonu vidět, na kterém hřišti hraje můj oblíbený tým, abych stihl začátek zápasu.
- Jako trenér chci po skončení turnaje vygenerovat diplomy pro první tři místa přímo z aplikace.
