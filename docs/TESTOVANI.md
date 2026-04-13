# Protokol o testování

Tento dokument sumarizuje postupy a výsledky ověřování funkčnosti Turnajového systému. Cílem testování bylo prokázat stabilitu aplikace a správnost výpočtů herní logiky.

## 1. Metodika testování
Aplikace prošla dvěma fázemi testování:
1. **Jednotkové (Unit) testy:** Automatizované testy v jazyce Python (pomocí knihovny `pytest`) ověřující izolované části backendu.
2. **Uživatelské (UX) testování:** Nasazení v reálném prostředí a testování koncovým uživatelem na mobilním zařízení během simulovaného turnaje.

## 2. Testy backendové logiky

### 2.1 Generování harmonogramu (Algoritmus bez kolizí)
* **Cíl testu:** Ověřit, že vygenerovaný rozvrh neobsahuje časové ani prostorové kolize.
* **Vstupní data:** 10 týmů, 2 dostupná hřiště, herní systém "Každý s každým".
* **Očekávaný výsledek:** Žádný tým nehraje dva zápasy v jeden čas a v daném čase neprobíhají více než 2 zápasy.
* **Výsledek:** Test proběhl úspěšně. Algoritmus správně nasadil čekací periody.

### 2.2 Přepočet průběžných tabulek
* **Cíl testu:** Ověřit správnost výpočtu bodů a stanovení pořadí při shodě bodů.
* **Vstupní data:** Zadání tří výsledků do skupiny, z toho dvě remízy.
* **Očekávaný výsledek:** Tabulka se seřadí primárně podle zisku bodů, sekundárně podle rozdílu skóre.
* **Výsledek:** Test proběhl úspěšně. Data vrácená přes API odpovídají manuálnímu výpočtu.

## 3. Uživatelské testování (Realné prostředí)

Aplikace byla testována na mobilním telefonu Samsung Galaxy a tabletu Apple iPad v hlučném prostředí sportovní haly.

| Identifikátor testu | Testovaná činnost | Výsledek a zjištění | Řešení / Úprava |
| :--- | :--- | :--- | :--- |
| UX-01 | Čitelnost UI na slunci | Nízký kontrast prvků při prohlížení venku. | Zvýšen kontrast tabulek, zaveden výraznější font. |
| UX-02 | Zápis skóre na dotykové obrazovce | Uživatel se často překlikl při zadávání dvouciferných hodnot. | Nahrazeno klasické vstupní pole za velká tlačítka `+` a `-` pro bezpečnější zápis. |
| UX-03 | Obnova přístupu (Local Storage) | Potvrzeno, že zavření a znovunačtení prohlížeče zachová administrátorská práva. | Funkce pracuje správně bez nutnosti úprav. |

## 4. Závěrečné zhodnocení
Provedené testy prokázaly plnou funkčnost klíčových algoritmů. Uživatelské testování pomohlo odhalit a následně odstranit nedostatky v responzivním chování klientské aplikace. Systém je stabilní a plně připraven pro nasazení v reálném provozu.