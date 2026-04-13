# Analýza projektu

Tento dokument obsahuje analýzu cílové skupiny, mapu uživatelských činností a definici základních pojmů Turnajového systému.

## 1. Analýza cílové skupiny

### 1.1 Charakteristika uživatele
Hlavním uživatelem systému je organizátor sportovní události (trenér, učitel, dobrovolník).
* **Odbornost:** Běžná uživatelská znalost práce s webovým prohlížečem.
* **Psychologický stav:** Uživatel se nachází ve stresu, v časové tísni a vyžaduje okamžité vyřešení problému bez studia dlouhých manuálů.
* **Cíl:** Chce rychle vytvořit rozpis zápasů a průběžně zadávat výsledky na mobilním zařízení.

### 1.2 Podmínky užití
Aplikace je určena pro nasazení přímo v dějišti turnaje (sportovní haly, hřiště).
* **Zařízení:** Primárně mobilní telefony a tablety.
* **Vnější vlivy:** Hluk, omezená pozornost uživatele, potřeba rychlého zápisu.

## 2. Mapa činností (Use Case)

### 2.1 Role: Administrátor (Organizátor)
Správce turnaje disponuje oprávněním k zápisu a modifikaci dat.
* **Založení turnaje:** Definice názvu, typu sportu a volba herního systému.
* **Správa účastníků:** Přidávání týmů a nahrávání log.
* **Generování harmonogramu:** Automatizované vytvoření časového plánu zápasů.
* **Záznam výsledků:** Průběžné zadávání skóre odehraných utkání.
* **Vyhlášení výsledků:** Export účastnických diplomů ve formátu PDF.

### 2.2 Role: Divák
Divák přistupuje k informacím v režimu pouze pro čtení (Read-only).
* **Sledování rozpisu:** Prohlížení plánovaných časů a hřišť.
* **Kontrola tabulek:** Sledování průběžného pořadí a výsledků.

## 3. Slovník pojmů

* **Admin Token:** Tajný identifikátor umožňující administrátorský přístup k turnaji.
* **Public UUID:** Veřejný identifikátor určený pro sdílení výsledků s diváky.
* **Harmonogram:** Časový a prostorový plán zápasů turnaje.
* **Pavouk:** Grafické znázornění vyřazovací části turnaje (Play-off).
* **Hrací systém:** Způsob utkání (např. každý s každým, skupinový systém).