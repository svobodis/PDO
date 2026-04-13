# Technické koncepty a architektura

Tento dokument vysvětluje vnitřní logiku Turnajového systému, architekturu aplikace a způsob správy dat. Porozumění těmto konceptům je nezbytné pro případné rozšiřování systému nebo jeho údržbu.

## 1. Architektura Klient-Server

Systém využívá moderní architekturu rozdělenou na dvě nezávislé vrstvy komunikující prostřednictvím bezestavového rozhraní REST API.

### 1.1 Klientská část (Frontend)
Frontend je realizován jako Single Page Application (SPA) v knihovně React.
* **Zodpovědnost:** Vykreslování uživatelského rozhraní, validace vstupů na straně klienta a správa lokálního stavu.
* **Komunikace:** Klient odesílá asynchronní HTTP požadavky na server a zpracovává odpovědi ve formátu JSON.
* **Výhoda:** Plynulý uživatelský zážitek bez nutnosti opětovného načítání celé stránky při každé interakci.

### 1.2 Serverová část (Backend)
Backend běží na frameworku Flask (Python).
* **Zodpovědnost:** Implementace herní logiky, algoritmy pro rozlosování zápasů, komunikace s databází a zabezpečení dat.
* **Bezestavovost:** Server neukládá informace o relaci (session). Každý požadavek musí obsahovat všechny informace potřebné k jeho vyřízení (např. Admin Token).

## 2. Správa přístupů bez registrace

Unikátním konceptem systému je absence klasických uživatelských účtů. Toto řešení maximalizuje rychlost nasazení turnaje v terénu.

### 2.1 Admin Token
Při vytvoření turnaje systém vygeneruje unikátní tajný klíč (token).
* **Funkce:** Token slouží jako autorizační prvek pro veškeré zápisové operace (CRUD).
* **Uložení:** Token je automaticky uložen v Local Storage prohlížeče organizátora. Tím je zajištěno, že při zavření prohlížeče nedojde ke ztrátě přístupu.
* **Záchrana přístupu:** Pro administraci z jiného zařízení musí uživatel tento token ručně přenést (např. pomocí funkce Načíst turnaj).

### 2.2 Public UUID
Veřejný identifikátor slouží pro sdílení dat s diváky.
* **Omezení:** Rozhraní přístupné přes UUID blokuje veškeré editační prvky.
* **Bezpečnost:** API na straně serveru odmítne jakýkoliv požadavek na změnu dat, pokud není doprovázen platným Admin Tokenem, i když útočník zná Public UUID.

## 3. Relační datový model

Data jsou organizována v relační struktuře, která zrcadlí hierarchii sportovní události.

### 3.1 Entity a vazby
* **Turnaj (Tournament):** Kořenová entita obsahující globální nastavení a oba přístupové klíče.
* **Tým (Team):** Entita vázaná na konkrétní turnaj (vazba 1:N). Obsahuje název a referenci na logo.
* **Skupina (Group):** Logický prvek pro herní systémy typu "základní skupiny". Propojuje týmy a definuje jejich vzájemné pořadí.
* **Zápas (Match):** Centrální entita propojující dva týmy, čas konání a výsledek. Zápas je vždy součástí turnaje a volitelně konkrétní skupiny.

### 3.2 Algoritmus rozlosování
Algoritmus generuje harmonogram tak, aby splnil tři kritéria:
1. Žádný tým nehraje více zápasů v jeden čas.
2. V jeden moment neprobíhá více zápasů, než kolik je dostupných hřišť.
3. Jsou dodrženy minimální přestávky mezi zápasy stejného týmu pro regeneraci hráčů.