# Reference aplikačního rozhraní (API)

Tento dokument definuje základní komunikační rozhraní (REST API) mezi klientskou aplikací (frontend) a serverem (backend). Veškerá datová výměna probíhá ve formátu JSON.

## 1. Konvence a autentizace
* **Základní URL:** `https://api.vasedomena.cz/api/v1`
* **Zabezpečení:** Většina editačních koncových bodů vyžaduje autorizaci pomocí `Admin Tokenu`. Tento token musí být přiložen v hlavičce HTTP požadavku: `Authorization: Bearer <token>`.
* **Identifikace:** Čtecí koncové body pro diváky vyžadují specifikaci `Public UUID` v parametrech cesty.

## 2. Přehled koncových bodů (Endpoints)

### 2.1 Turnaj
* **Vytvoření nového turnaje**
  * **Metoda:** `POST /tournaments`
  * **Tělo (Request):** JSON objekt s názvem, typem sportu a herním formátem.
  * **Odpověď (Response):** `201 Created` – vrací vygenerovaný `Admin Token` a `Public UUID`.
* **Načtení dat pro diváky**
  * **Metoda:** `GET /tournaments/public/<uuid>`
  * **Odpověď (Response):** `200 OK` – vrací kompletní data turnaje (bez editačních oprávnění).

### 2.2 Týmy
* **Přidání týmu**
  * **Metoda:** `POST /tournaments/<token>/teams`
  * **Tělo (Request):** JSON objekt s názvem týmu a volitelným logem.
  * **Odpověď (Response):** `201 Created` – vrací ID nového týmu.
* **Smazání týmu**
  * **Metoda:** `DELETE /tournaments/<token>/teams/<team_id>`
  * **Odpověď (Response):** `204 No Content` – potvrzuje úspěšné smazání.

### 2.3 Rozvrh a zápasy
* **Generování harmonogramu**
  * **Metoda:** `POST /tournaments/<token>/schedule/generate`
  * **Tělo (Request):** Parametry pro generování (počet hřišť, délka zápasu).
  * **Odpověď (Response):** `200 OK` – spouští algoritmus a vrací vygenerovaný časový plán.
* **Zápis výsledku**
  * **Metoda:** `PUT /tournaments/<token>/matches/<match_id>/score`
  * **Tělo (Request):** JSON objekt s finálním skóre (např. `{"team1_score": 3, "team2_score": 1}`).
  * **Odpověď (Response):** `200 OK` – přepočítá body a aktualizuje tabulky.

## 3. Chybové stavy
Rozhraní vrací standardní HTTP chybové kódy:
* `400 Bad Request:` Neplatná data v požadavku.
* `401 Unauthorized:` Chybějící nebo neplatný Admin Token.
* `404 Not Found:` Požadovaný zdroj (např. turnaj podle UUID) neexistuje.
* `500 Internal Server Error:` Interní chyba při výpočtu (např. selhání algoritmu rozlosování).