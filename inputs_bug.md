# 🛠 Technický Bug Report: Správa firmy (Aktualizované)

Tento dokument sumarizuje chyby v module **Správa firmy**. 

> [!WARNING]
> **Hlavná požiadavka:** Nižšie popísanú logiku spracovania číselných vstupov je potrebné aplikovať **globálne** na všetky inputy v aplikácii, kde dochádza k tomuto glitchu, alebo vytvoriť znovupoužiteľný komponent.

---

## 🔴 1. KRITICKÁ CHYBA: Strata dát pri navigácii
- **Popis:** Pri prepínaní medzi tabmi (napr. zo "Správa firmy" do "Správa používateľov" a späť) sa neuložené zmeny stratia.
- **Očakávané správanie:** Implementovať perzistenciu stavu (lifting state up / Context API / URL params), aby používateľ neprišiel o rozpracované dáta.

---

## 🟡 2. GLOBÁLNY REFRAKTORING: Oprava Input logiky

### Problém: "Zaseknutá nula / Hardcoded správanie"
Identifikovali sme, že komponenty typu `number` trpia spoločnou chybou: `onChange` handler nasilu vracia `0`, keď používateľ vymaže pole (backspace). To znemožňuje prirodzenú editáciu.

**Chybný prístup (Aplikovaný teraz):**
```javascript
per_invoice_created: e.target.value === '' ? 0 : parseFloat(e.target.value)
