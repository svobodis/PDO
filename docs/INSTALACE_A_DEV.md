# Instalace a nasazení (Návod pro vývojáře)

Tento dokument popisuje postup pro lokální zprovoznění Turnajového systému za účelem vývoje a testování a následný postup pro nasazení do produkčního prostředí.

## 1. Zprovoznění lokálního serveru (Backend)

**Než začnete:** Zkontrolujte, že máte ve svém systému nainstalován jazyk Python (verze 3.8 nebo vyšší) a stažený zdrojový kód repozitáře.

Pro spuštění backendové části:
1. Otevřete příkazový řádek a přejděte do kořenové složky projektu.
2. Přesuňte se do složky backendu:
   `cd backend`
3. Vytvořte izolované virtuální prostředí:
   `python -m venv venv`
4. Aktivujte virtuální prostředí:
   * Windows: `venv\Scripts\activate`
   * macOS/Linux: `source venv/bin/activate`
5. Nainstalujte požadované závislosti:
   `pip install -r requirements.txt`
6. Spusťte vývojový Flask server:
   `flask run`
Server běží a naslouchá na adrese `http://127.0.0.1:5000`.

## 2. Zprovoznění uživatelského rozhraní (Frontend)

**Než začnete:** Ověřte, že máte nainstalované prostředí Node.js (verze 16 nebo vyšší) a správce balíčků npm. Backendový server z předchozího postupu musí běžet na pozadí.

Pro spuštění frontendové části:
1. Otevřete nové okno příkazového řádku a přejděte do kořenové složky projektu.
2. Přesuňte se do složky frontendu:
   `cd frontend`
3. Nainstalujte všechny potřebné JavaScriptové knihovny:
   `npm install`
4. Zkontrolujte soubor `.env.local` a ověřte, že proměnná pro API směřuje na váš lokální server (např. `REACT_APP_API_URL=http://127.0.0.1:5000`).
5. Spusťte vývojový server Reactu:
   `npm start`
Aplikace se automaticky otevře ve výchozím webovém prohlížeči na adrese `http://localhost:3000`.

## 3. Nasazení do produkčního prostředí (Deployment)

Systém je navržen pro běh na bezplatných cloudových platformách.

### 3.1 Nasazení Backend API (PythonAnywhere)
1. Přihlaste se do portálu PythonAnywhere a přejděte na záložku **Web**.
2. Zvolte **Add a new web app** a vyberte framework Flask s vaší verzí Pythonu.
3. V záložce **Consoles** otevřete terminál a naklonujte repozitář s vaším kódem.
4. Nastavte cestu k virtuálnímu prostředí a nainstalujte závislosti ze souboru `requirements.txt`.
5. V sekci **Web** upravte konfigurační soubor WSGI tak, aby importoval vaši aplikaci.
6. Stiskněte tlačítko **Reload**.
Backend je dostupný na vaší přidělené subdoméně (např. `https://vas-ucet.pythonanywhere.com`).

### 3.2 Nasazení Frontendu (Vercel)
**Než začnete:** Zkopírujte si URL adresu nasazeného backendu z předchozího kroku.

1. Přihlaste se do platformy Vercel a zvolte **Add New Project**.
2. Propojte svůj GitHub účet a importujte repozitář s projektem.
3. V sekci **Environment Variables** vytvořte novou proměnnou `REACT_APP_API_URL` a jako hodnotu zadejte URL adresu vašeho produkčního backendu.
4. Stiskněte tlačítko **Deploy**.
Vercel automaticky zkompiluje aplikaci a přidělí jí veřejnou URL adresu s HTTPS certifikátem.