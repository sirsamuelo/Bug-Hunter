# Prehľad úprav a chýb v systéme

---

## ## Nastavenia
* **Perzistencia stavu:** Opraviť ukladanie rozpracovanej práce. Pri prepnutí okna alebo aplikácie systém stratí dáta a vráti používateľa na úvodnú obrazovku nastavení.
* **Vytváranie používateľov:** Aktuálne nefunkčné. Pri tvorbe nového konta sa nezobrazujú tímy (pravdepodobne sú tam statické dáta). Je potrebné implementovať výber z existujúcich tímov.
* **Reorganizácia navigácie:** Zlúčiť sekcie **Nastavenia** a **Nastavenia tímov**. Položku „Nastavenia tímov“ následne odstrániť zo sidebaru pre vyššiu prehľadnosť.

## ## Permaguard
* **Vizuál statusov:** Redizajnovať label statusu **"V preprave"**, momentálne pôsobí esteticky rušivo.

## ## POP
* **Umiestnenie v menu:** Keďže ide o zriedka využívaný prístup, presunúť túto sekciu zo sidebaru do **Nastavenia -> Nastavenia pravidelných preprav**, aby nezaberala miesto v hlavnom menu.

## ## Objednávky
* **Fix eventov (Bubbling):** Pri kliknutí na „Kopírovať“ v menu (...) systém nesmie presmerovať na detail objednávky. Použiť `Event.stopPropagation()`.
* **Definícia procesov:** Jasne špecifikovať, čo presne predstavuje entita **„Nová objednávka“**.
* **UX vylepšenia:**
    * Pridať **tooltipy** pre skratky: **ADR** (nebezpečný tovar/licencie) a **FTL** (full truck load).
    * Nahradiť manuálne zadávanie dátumov za **datepicker** (prevencia chýb v PDF).
* **Logika financií:** Input „Extra disponent“ uzamknúť (**disabled**) až do momentu, kým nie sú kompletne nacenené sumy za prepravu a od klienta.
* **PDF Generovanie:** Opraviť kritickú chybu zobrazovania dátumov. Aktuálne generuje `NaN-NaN-NaN`.
* **KRITICKÝ BUG (Refresh):** Systém pri prepnutí okna/tabu v prehliadači samovoľne resetuje zobrazenie na predvolený tab (napr. z „Financií“ späť na „Dopravné detaily“). Tento problém je globálny.
* **Business validácia:** Zvážiť, či je prípustné vytvoriť objednávku bez kompletne zadaných finančných detailov.

## ## Filters - Objednávky
* **Nefunkčné filtre:** Opraviť filtrovanie podľa **Klienta** a **Obchodníka** – zmena filtra aktuálne nijak neovplyvňuje zobrazené dáta.
* **Zjednotenie logiky:** Konsolidovať statusy fakturácie. Aktuálne sú rozdelené nelogicky (v jednom filtri: Vyfakturované/Odovzdané, v druhom: Draft/Fakturované/Zaplatené). Spojiť do jednej prehľadnej štruktúry.
