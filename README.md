# Symulator Podatków CIT i VAT — landing page

Strona udostępniająca instalator aplikacji desktopowej **Symulator Podatków CIT
i VAT** (dla biur architektonicznych, PKD 71.11.Z). Wzór: landing WhisperVoice
(`powtarzasie/mojatranskrypcja`).

- **Strona:** `index.html` → hostowana przez **GitHub Pages**.
- **Instalator `.exe` (~98 MB):** hostowany przez **GitHub Releases** (nie w repo).
- **Licznik pobrań:** pobierany na żywo z GitHub Releases API.

---

## Publikacja — krok po kroku

### 1. Utwórz repozytorium
Nazwa zgodna z konfiguracją w `index.html`: **`symulator-podatkow-landing`**
(na koncie `powtarzasie`). Jeśli wybierzesz inną nazwę — zmień stałą `REPO`
w `index.html` (sekcja `<script>`).

### 2. Wrzuć pliki strony
Skopiuj do repo: `index.html`, `README.md`, folder `.github/`.
Dodaj `og-image.jpg` (1200×630) — podgląd przy udostępnianiu w mediach
społecznościowych (strona działa też bez niego).

```bash
git init
git add .
git commit -m "Landing page Symulator Podatkow CIT i VAT"
git branch -M main
git remote add origin https://github.com/powtarzasie/symulator-podatkow-landing.git
git push -u origin main
```

### 3. Włącz GitHub Pages
Repo → **Settings → Pages** → *Source: Deploy from a branch* → branch **main**,
folder **/ (root)** → Save. Po chwili strona będzie pod:
`https://powtarzasie.github.io/symulator-podatkow-landing/`

### 4. Opublikuj instalator jako Release
Utwórz i wypchnij tag — workflow `create-release.yml` utworzy wydanie:
```bash
git tag v1.0.0
git push origin v1.0.0
```
Następnie **dołącz plik `.exe` do wydania** (jeden z dwóch sposobów):

- **Przez stronę:** repo → *Releases* → `v1.0.0` → *Edit* → przeciągnij
  `Symulator Podatkow CIT i VAT Setup 1.0.0.exe` w pole assetów → *Update release*.
- **Przez CLI:**
  ```bash
  gh release upload v1.0.0 "C:\ClaudeSANDDBOX\AI_Ksiegowy\release\Symulator Podatkow CIT i VAT Setup 1.0.0.exe"
  ```

> Plik instalatora powstaje w repo aplikacji (`AI_Ksiegowy`) komendą
> `npm run electron:build` → folder `release\`. Tutaj trzymamy tylko stronę.

### 5. Sprawdź
- [ ] Strona ładuje się pod adresem Pages.
- [ ] Przycisk „Pobierz” pobiera właściwy `.exe` z Release.
- [ ] Licznik „Pobrań” pokazuje liczbę (po pierwszych pobraniach).
- [ ] Zastrzeżenie podatkowe jest widoczne na stronie.
- [ ] Podgląd linku (OG) wygląda poprawnie po wklejeniu w social media.

---

## Aktualizacja do nowej wersji
1. Zbuduj nowy `.exe` w repo aplikacji.
2. Wypchnij nowy tag (np. `v1.1.0`) → workflow utworzy nowe wydanie.
3. Dołącz nowy `.exe` do wydania.
4. Zaktualizuj w `index.html`: stałą `TAG`, `FALLBACK_URL`, numer wersji i rozmiar
   w przycisku/modalu.

## Konfiguracja w `index.html`
W sekcji `<script>` na dole pliku:
```js
const REPO = "powtarzasie/symulator-podatkow-landing";
const TAG  = "v1.0.0";
const FALLBACK_URL = `https://github.com/${REPO}/releases/download/${TAG}/Symulator.Podatkow.CIT.i.VAT.Setup.1.0.0.exe`;
```
(GitHub w adresie pobierania zamienia spacje w nazwie pliku na kropki — dlatego
`FALLBACK_URL` ma kropki. Skrypt i tak najpierw pobiera prawdziwy URL z API.)

## Licencja
Strona i aplikacja: MIT © 2026 Mariusz Świergula.
