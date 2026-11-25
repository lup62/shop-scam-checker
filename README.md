# 🔍 Shop Scam Checker

Una skill per [Claude](https://claude.ai) che analizza un sito e-commerce e assegna un punteggio di affidabilità (0–100) per verificare se è uno scam.

## Cosa fa

Dato un URL di un negozio online, la skill esegue un'analisi approfondita su 10 segnali:

| Segnale | Cosa verifica |
|---|---|
| **SSL/HTTPS** | Presenza del certificato di sicurezza |
| **Età dominio** | Da quanto tempo esiste il sito (WHOIS) |
| **Contatti** | Indirizzo, telefono, email, P.IVA — e se la P.IVA è copiata da un'altra azienda |
| **Policy legali** | Privacy Policy, Termini e Condizioni, Resi |
| **Metodi pagamento** | PayPal, carta con protezione, o solo bonifico/crypto |
| **Recensioni esterne** | Trustpilot, Google Reviews, Reddit |
| **Prezzi** | Confronto con Amazon e store ufficiali |
| **Qualità contenuti** | Testi originali o copiati, errori, recensioni fake |
| **Social media** | Profili attivi e reali o assenti/fake |
| **Segnalazioni scam** | Presenza in blacklist, forum, segnalazioni online |

### Verdetti

- 🟢 **AFFIDABILE** (80–100)
- 🟡 **PROCEDERE CON CAUTELA** (50–79)
- 🟠 **SOSPETTO** (25–49)
- 🔴 **PROBABILE SCAM** (0–24)

## Installazione

### Requisiti

- Un account [Claude Pro, Team o Enterprise](https://claude.ai) con le **Skills** abilitate

### Passaggi

1. Apri [claude.ai](https://claude.ai)
2. Vai in **Impostazioni** → **Skills**
3. Clicca **"Aggiungi skill"** (o "Add skill")
4. Clicca **"Crea skill"** (o "Create skill")
5. Compila i campi:
   - **Nome**: `shop-scam-checker`
   - **Descrizione**: `Analyze an online shop URL and score its trustworthiness — use when the user asks to check if a website or shop is a scam, legit, or trustworthy.`
   - **Istruzioni (SKILL.md)**: copia e incolla il contenuto del file [`SKILL.md`](./SKILL.md) di questa repo
6. Salva

### Uso

In una chat con Claude, scrivi semplicemente:

```
/shop-scam-checker esempio-shop.com
```

Oppure chiedi in linguaggio naturale:

```
Puoi verificare se questo sito è affidabile? https://esempio-shop.com
```

```
È uno scam questo sito? esempio-shop.it
```

Claude riconoscerà automaticamente la richiesta e attiverà la skill.

### Output di esempio

La skill produce un report dettagliato come questo:

```
🔍 Shop Scam Check: esempio-shop.com

Punteggio di affidabilità: 22/100

Verdetto: 🔴 PROBABILE SCAM

┌─────────────────────┬─────────────────────────────┬──────────┐
│ Segnale              │ Trovato                     │ Punti    │
├─────────────────────┼─────────────────────────────┼──────────┤
│ SSL/HTTPS            │ Presente                    │ +5       │
│ Età dominio          │ < 6 mesi                    │ -15      │
│ Contatti             │ Solo email, P.IVA copiata   │ -15      │
│ ...                  │ ...                         │ ...      │
└─────────────────────┴─────────────────────────────┴──────────┘

⚠️ Red flags trovate
• Prezzi irrealistici (iPhone 16 a 200€)
• P.IVA copiata da un'azienda non correlata
• ...

✅ Segnali positivi
• SSL presente
• ...

💡 Consiglio
Non acquistare su questo sito. [motivazione personalizzata]
```

## File

- [`README.md`](./README.md) — Questa documentazione
- [`SKILL.md`](./SKILL.md) — Le istruzioni della skill (da copiare in Claude)

## Licenza

MIT
