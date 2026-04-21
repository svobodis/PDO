# Turnajový systém

Webová aplikace pro automatizované generování harmonogramů a komplexní správu amatérských sportovních turnajů. Projekt je zaměřen na maximální rychlost nasazení v terénu bez nutnosti registrace uživatelů.

## Návod pro oponenta
Tato sekce slouží k rychlému ověření funkčnosti a kvality odevzdaného řešení.

### Živé demo (Produkční prostředí)
Aplikaci si prohlédněte přímo v prohlížeči bez nutnosti lokální instalace:
* **Uživatelské rozhraní (Frontend):** https://app-tournaments.vercel.app
* **Aplikační rozhraní (Backend API):** https://jan-svoboda.pythonanywhere.com

### Práce s testovacími daty
Pro účely testování využijte připravená data, která simulují probíhající házenkářský turnaj:
1. Na úvodní stránce do pole **Načíst turnaj** vložte testovací token: `246b82fb-546b-402c-a7f3-571fe5a970b4`.
2. Prohlédněte si automaticky vygenerovaný rozvrh zápasů a průběžné tabulky.
3. Vyzkoušejte zadání výsledku u plánovaného zápasu a sledujte okamžitý přepočet bodů.

## Struktura repozitáře
Zdrojové kódy jsou rozděleny podle architektury Klient-Server:
* `/frontend`: Klientská aplikace v React.js (uživatelské rozhraní).
* `/backend`: Serverová část v Python/Flask (aplikační logika a algoritmy).
* `/docs`: Kompletní projektová dokumentace ve formátu Markdown.

## Rozcestník dokumentace
Pro detailní pochopení systému využijte následující dokumenty:
* [Analýza](docs/ANALYZA.md): Popis cílové skupiny.
* [Koncepty a architektura](docs/KONCEPTY.md): Vysvětlení správy přístupů bez registrace a datového modelu.
* [Příručka organizátora](docs/PRIRUCKA_ORGANIZATORA.md): Návod pro koncové uživatele.
* [Instalační příručka](docs/INSTALACE_A_DEV.md): Postup pro lokální zprovoznění vývojového prostředí.
* [Reference API](docs/REFERENCE_API.md): Technický popis všech dostupných endpointů.

---
**Autor:** Jan Svoboda (jan.svoboda1@tul.cz)
**Vedoucí:** Ing. Vratislav Žabka, Ph.D.
**Rok:** 2025/26
