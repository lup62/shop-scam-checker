---
name: "shop-scam-checker"
description: "Analyze an online shop URL and score its trustworthiness — use when the user asks to check if a website or shop is a scam, legit, or trustworthy."
---

# Shop Scam Checker

Analizza un sito e-commerce e assegna un punteggio di affidabilità (0–100) basato su molteplici segnali.

## Quando usare

Quando l'utente chiede di verificare se un sito/shop online è affidabile, legittimo o una truffa.

## Input

L'utente fornisce un URL di un sito e-commerce da analizzare.

## Procedura

### 1. Raccolta dati sul sito

Esegui queste ricerche in parallelo dove possibile:

1. **Visita il sito** — Usa WebFetch sull'URL fornito. Analizza:
   - Presenza di pagine legali: Privacy Policy, Terms & Conditions, Return/Refund Policy
   - Informazioni di contatto: indirizzo fisico, email, telefono, partita IVA / company number
   - **Verifica P.IVA / company number copiata**: i siti scam spesso copiano la P.IVA di un'azienda reale per sembrare legittimi. Controlla:
     - Se la ragione sociale nel footer corrisponde a quella nella Privacy Policy e nelle altre pagine legali
     - Se cercando la P.IVA online si trova un'azienda diversa (es. un seller Amazon, un altro sito) che non ha alcun legame dichiarato col sito analizzato
     - Se esiste un link incrociato tra il sito e l'azienda titolare della P.IVA (es. il seller Amazon linka al sito e viceversa)
     - Se la pagina "Chi siamo" o "About" è assente, vuota o restituisce errore
     - Se l'azienda reale titolare della P.IVA opera in un settore completamente diverso
   - Metodi di pagamento accettati (carta, PayPal, bonifico, crypto)
   - Qualità generale del sito (testo copiato, errori grammaticali, immagini stock)
   - Presenza di certificato SSL (https)
   - Prezzi: se sono troppo bassi rispetto al mercato (segnale di scam)

2. **Ricerca reputazione esterna** — Fai WebSearch per:
   - `"nome-dominio" reviews` oppure `"nome-dominio" scam`
   - `"nome-dominio" trustpilot` o altre piattaforme di recensioni
   - `site:reddit.com "nome-dominio"` per opinioni degli utenti
   - Cerca se il dominio appare in blacklist note o segnalazioni di truffe

3. **Analisi dominio** — Fai WebSearch per:
   - Età del dominio (WHOIS lookup) — cerca `whois nome-dominio`
   - Informazioni sul registrante (se pubbliche)
   - Se il dominio è molto recente (< 6 mesi) è un segnale negativo

4. **Confronto prezzi** — Se il sito vende prodotti riconoscibili (brand noti):
   - Cerca i prezzi degli stessi prodotti su Amazon/store ufficiali
   - Sconti superiori al 70-80% su prodotti di marca sono un forte segnale di scam

### 2. Valutazione — Checklist dei segnali

Assegna punti per ogni categoria (il punteggio parte da 50 e viene modificato):

| Segnale | Affidabile | Sospetto | Red flag |
|---|---|---|---|
| **SSL/HTTPS** | +5 (presente) | — | -10 (assente) |
| **Età dominio** | +10 (> 2 anni) | +0 (6 mesi–2 anni) | -15 (< 6 mesi) |
| **Contatti** | +10 (indirizzo, tel, email, P.IVA verificata) | +0 (solo email) | -15 (nessun contatto o P.IVA copiata da altra azienda) |
| **Policy legali** | +5 (complete e dettagliate) | +0 (generiche/copiate) | -10 (assenti) |
| **Metodi pagamento** | +5 (PayPal, carta con protezione) | +0 (solo carta) | -10 (solo bonifico/crypto) |
| **Recensioni esterne** | +10 (positive su Trustpilot/Google) | +0 (nessuna) | -15 (negative o segnalazioni scam) |
| **Prezzi** | +5 (in linea col mercato) | +0 (sconti ragionevoli) | -15 (troppo belli per essere veri) |
| **Qualità contenuti** | +5 (testi originali, ben scritti) | +0 (nella media) | -10 (errori, testi copiati, lorem ipsum) |
| **Social media** | +5 (profili attivi e reali) | +0 (presenti ma inattivi) | -5 (assenti o fake) |
| **Segnalazioni scam** | +5 (nessuna) | — | -20 (presenti su forum/blacklist) |

### 3. Output — Report finale

Presenta il risultato in questo formato:

```
## 🔍 Shop Scam Check: [nome sito]

**Punteggio di affidabilità: XX/100**

**Verdetto:** [uno dei seguenti]
- 🟢 AFFIDABILE (80–100)
- 🟡 PROCEDERE CON CAUTELA (50–79)  
- 🟠 SOSPETTO (25–49)
- 🔴 PROBABILE SCAM (0–24)

### Dettaglio analisi

[Tabella con ogni segnale analizzato, cosa è stato trovato, e il punteggio assegnato]

### ⚠️ Red flags trovate
[Lista dei segnali negativi più importanti, se presenti]

### ✅ Segnali positivi
[Lista dei segnali positivi trovati, se presenti]

### 💡 Consiglio
[Raccomandazione finale personalizzata basata sull'analisi]
```

### 4. Condivisione del report

Dopo aver presentato il report, chiedi all'utente se vuole una versione esportabile. Se l'utente accetta o lo chiede esplicitamente (es. "dammi il report", "voglio condividerlo", "mandamelo"), genera:

- Un **messaggio pronto da copiare e incollare** — versione compatta del report con punteggio, verdetto, red flags principali e consiglio finale, formattata in modo leggibile anche su WhatsApp/Telegram (senza markdown pesante)

Oppure, se l'utente lo preferisce:

- Un **file** (.md o .txt) con il report completo e dettagliato, inclusa la tabella dei segnali

### Note importanti

- Specifica sempre che questa è un'analisi automatizzata e non una garanzia assoluta
- Se non riesci ad accedere al sito (down, bloccato, geo-restricted), segnalalo e basa l'analisi sui dati esterni disponibili
- Sii oggettivo: non esagerare né in positivo né in negativo
- Se il sito è chiaramente un grande retailer noto (Amazon, eBay, ecc.), segnalalo subito senza analisi completa