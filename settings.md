# 🛠 Report technických chýb: Správa firmy

Tento dokument slúži ako podklad pre vývojový tím na odstránenie chýb v module **Správa firmy**.

---

## 🔴 KRITICKÉ CHYBY (CRITICAL) - FIXNUTE 12.2.2026 / treba test 

### 1. Strata stavu pri prepínaní tabov (State Management)
- **Lokalita:** Modul "Správa firmy" (všetky taby)
- **Popis:** Ak používateľ edituje údaje v tabe "Správa firmy" a následne klikne na iný tab (napr. "Správa používateľov") a vráti sa späť, všetky vykonané zmeny sú premazané.
- **Chybné správanie:** Systém pri návrate automaticky presmeruje používateľa na tab "Správa používateľov" namiesto rozpracovaného tabu.
- **Očakávané správanie:** Rozpracované dáta musia ostať zachované v pamäti (state) a navigácia musí zachovať kontext pôvodného tabu.

---

## 🟡 FUNKČNÉ CHYBY (BUGS) - FIXNUTE 12.2.2026 / treba test 

### 1. Sekcia: Viditeľnosť (Toggles)
- **DPH Breakdown:** Prepínač (toggle) pre rozpis DPH nevykonáva žiadnu akciu.
- **Cena dopravcu:** Prepínač pre zobrazenie ceny dopravcu je nefunkčný.

### 2. Sekcia: Financie (Input Logic) - FIXNUTE 12.2.2026 / treba test  
- **Splatnosť faktúr:** V poli pre počet dní je hodnota "zaseknutá" (pravdepodobne hardcoded). Pri pokuse o zmenu sa hodnota resetuje na číslo 6 alebo 60.
- **Provízie (Chyba komponentu):** - **Problém:** V číselných vstupoch nie je možné úplne vymazať hodnotu "0". Backspace nefunguje na odstránenie poslednej nuly.
    - **Požiadavka:** Odstrániť tento glitchy komponent a nahradiť ho štandardným číselným vstupom, ktorý umožňuje prázdnu hodnotu (null/empty).

---

## 🔵 UI A VIZUÁLNE CHYBY (UI/UX)

| Komponent | Popis chyby | Očakávaný stav |
| :--- | :--- | :--- |
| **Tab: Vzhľad** | Pozícia loga "Middle" (na stred) nefunguje. | Logo sa musí vycentrovať podľa nastavenia. |
| **Náhľad dokumentu** | Zobrazuje sa zdvojená ikona krížika (double cross). | Odstrániť redundantnú ikonu z UI. |

---

> [!IMPORTANT]
> **Priorita riešenia:**
> 1. **State Management** (zamedzenie strate dát)
> 2. **Oprava Input komponentov** v sekcii Financie
> 3. **Oprava nefunkčných prepínačov**
