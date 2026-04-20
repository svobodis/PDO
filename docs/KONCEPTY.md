# Technické koncepty a architektonická rozhodnutí

Tento dokument vysvětluje vnitřní logiku systému, datové toky a technická rozhodnutí učiněná během vývoje.

## 1. Datový model a referenční integrita
Systém využívá relační databázi spravovanou skrze SQLAlchemy ORM. Architektura dat je navržena tak, aby byla zajištěna konzistence i při dynamických změnách turnaje.

- Hierarchie entit: `Tournament` -> `Group` -> `Team` -> `Match`.
- Entita `Match` je klíčovým propojovacím prvkem, který drží reference na dva týmy, konkrétní hřiště (`Field`) a časový slot.
- Referenční integrita: Smazání skupiny vede k uvolnění týmů do stavu bez přiřazení (group_id = NULL), nikoliv k jejich smazání.

## 2. Logika generování herních systémů
Aplikace deleguje tvorbu zápasů na specializované generátory ve složce `backend/generators/`. Každý systém má vlastní matematickou logiku:

- Round Robin (Každý s každým): Implementuje algoritmus zajišťující, že se každý tým utká s každým právě jednou.
- Knockout (Vyřazovací systém): Generuje strukturu s pevnými vazbami `next_match_id`. Vítěz zápasu je logikou backendu automaticky posouván do následujícího kola.
- Heuristika rozvrhování: Systém využívá "hladový" algoritmus, který iteruje nad množinou nezařazených zápasů a hledá pro ně nejbližší volný slot při dodržení kolizních podmínek (tým nemůže hrát dva zápasy najednou).

## 3. State Management na frontendu
Frontendová aplikace v Reactu nevyužívá pro správu dat lokální stavy jednotlivých komponent, ale centralizovaný `TournamentProvider`.

- Výhody: Jakákoliv komponenta (např. editace výsledku) má okamžitý přístup k globálním datům turnaje bez nutnosti předávání parametrů (prop drilling).
- Asynchronní operace: Veškerá komunikace s API je zapouzdřena do `useCallback` funkcí v rámci kontextu, což optimalizuje výkon a zabraňuje zbytečnému překreslování UI.

## 4. Strategie synchronizace (Polling)
Vzhledem k požadavku na živé výsledky v diváckém režimu bez nutnosti registrace uživatelů k odběru novinek (WebSockets) byla zvolena strategie "Short Polling".
- Komponenta `PublicView` v pravidelném pětisekundovém intervalu vyvolává asynchronní dotaz na endpoint `/api/tournaments/<uuid>`.
- Tento přístup zajišťuje vysokou kompatibilitu se staršími mobilními prohlížeči a minimalizuje režii spojenou s udržováním trvalého spojení na serveru.

## 5. Zpracování médií (Cloudinary Pipeline)
Nahrávání logotypů týmů nezatěžuje aplikační server binárními daty.
- Pipeline: Frontend odešle soubor na backend -> backend využije Cloudinary SDK pro upload -> Cloudinary provede transformaci (ořez 200x200px, optimalizace kvality) -> backend uloží pouze výslednou URL adresu.
- Výsledek: Rychlé načítání diváckého pohledu díky distribuci obrázků přes globální síť CDN.
