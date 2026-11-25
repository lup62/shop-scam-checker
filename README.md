# 🔍 Shop Scam Checker

A [Claude](https://claude.ai) skill that analyzes an e-commerce website and assigns a trustworthiness score (0–100) to determine if it's a scam.

🇮🇹 [Leggi in italiano](./README.it.md)

## What it does

Given an online store URL, the skill performs an in-depth analysis across 10 signals:

| Signal | What it checks |
|---|---|
| **SSL/HTTPS** | Security certificate present |
| **Domain age** | How long the site has existed (WHOIS) |
| **Contact info** | Address, phone, email, VAT number — and whether the VAT number is stolen from another business |
| **Legal pages** | Privacy Policy, Terms & Conditions, Returns |
| **Payment methods** | PayPal, card with buyer protection, or wire/crypto only |
| **External reviews** | Trustpilot, Google Reviews, Reddit |
| **Prices** | Comparison with Amazon and official stores |
| **Content quality** | Original or copied text, errors, fake reviews |
| **Social media** | Active real profiles or absent/fake |
| **Scam reports** | Presence on blacklists, forums, online reports |

### Verdicts

- 🟢 **TRUSTWORTHY** (80–100)
- 🟡 **PROCEED WITH CAUTION** (50–79)
- 🟠 **SUSPICIOUS** (25–49)
- 🔴 **LIKELY SCAM** (0–24)

## Installation

### Requirements

- A [Claude Pro, Team, or Enterprise](https://claude.ai) account with **Skills** enabled

### Steps

1. Open [claude.ai](https://claude.ai)
2. Go to **Settings** → **Skills**
3. Click **"Add skill"**
4. Click **"Create skill"**
5. Fill in the fields:
   - **Name**: `shop-scam-checker`
   - **Description**: `Analyze an online shop URL and score its trustworthiness — use when the user asks to check if a website or shop is a scam, legit, or trustworthy.`
   - **Instructions (SKILL.md)**: copy and paste the contents of the [`SKILL.md`](./SKILL.md) file from this repo
6. Save

### Usage

In a chat with Claude, simply type:

```
/shop-scam-checker example-shop.com
```

Or ask in natural language:

```
Can you check if this site is legit? https://example-shop.com
```

```
Is this website a scam? example-shop.com
```

Claude will automatically recognize the request and activate the skill.

### Example output

The skill produces a detailed report like this:

```
🔍 Shop Scam Check: example-shop.com

Trustworthiness score: 22/100

Verdict: 🔴 LIKELY SCAM

┌─────────────────────┬─────────────────────────────┬──────────┐
│ Signal               │ Found                       │ Score    │
├─────────────────────┼─────────────────────────────┼──────────┤
│ SSL/HTTPS            │ Present                     │ +5       │
│ Domain age           │ < 6 months                  │ -15      │
│ Contact info         │ Email only, stolen VAT ID   │ -15      │
│ ...                  │ ...                         │ ...      │
└─────────────────────┴─────────────────────────────┴──────────┘

⚠️ Red flags found
• Unrealistic prices (iPhone 16 at $200)
• VAT number copied from an unrelated company
• ...

✅ Positive signals
• SSL present
• ...

💡 Recommendation
Do not buy from this site. [personalized reasoning]
```

## Files

- [`README.md`](./README.md) — This documentation (English)
- [`README.it.md`](./README.it.md) — Documentazione in italiano
- [`SKILL.md`](./SKILL.md) — Skill instructions (copy into Claude)

## License

MIT
