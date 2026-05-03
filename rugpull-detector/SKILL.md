---
name: rugpull-detector
description: >
  Analysiert Kryptowährungen auf Rugpull-Risiken und Betrugszeichen. Verwende diesen Skill IMMER wenn:
  - Ein Nutzer fragt ob ein Coin/Token sicher ist, einen Rugpull-Score will, oder einen Coin analysieren möchte
  - Jemand einen Coin-Namen + Social Media Erwähnung nennt (z.B. "FOFAR wird von timclassified beworben")
  - Jemand fragt "Ist [Coin] ein Scam?", "Lohnt sich [Token]?", "Ist das ein Rugpull?"
  - Krypto-Coins mit verdächtigen Merkmalen erwähnt werden: unbekannte Tokens, Meme-Coins, neue Launches
  - On-Chain Analyse, Tokenomics-Check oder Influencer-Werbung für Kryptos untersucht werden soll
  Gibt einen detaillierten Rugpull-Report mit Score 0-100 und Ampelsystem zurück. Nutze diesen Skill auch proaktiv wenn du Betrugszeichen erkennst, auch wenn nicht explizit nach einem Score gefragt wird.
---

# Rugpull Detector Skill

## Überblick

Dieser Skill analysiert Kryptowährungs-Token systematisch auf Betrugs- und Rugpull-Indikatoren. Er kombiniert CoinMarketCap-Daten, Social Media Recherche, On-Chain Signale und News, um einen umfassenden Rugpull-Score zu berechnen.

---

## Schritt-für-Schritt Analyse-Workflow

### Schritt 1: CoinMarketCap & Basisdaten recherchieren
Suche via Web Search nach:
- `[COINNAME] coinmarketcap` → Preis, Marktkapitalisierung, Volumen/MarketCap-Ratio
- `[COINNAME] token contract` → Smart Contract Adresse
- `[COINNAME] crypto launch date` → Wie jung ist der Token?
- `[COINNAME] whitepaper team` → Gibt es ein Team/Whitepaper?

**Kritische Metriken:**
- Volume/MarketCap Ratio > 100% → **starkes Warnsignal** (künstliches Volumen)
- Coin < 30 Tage alt → **Warnsignal**
- Kein Whitepaper auffindbar → **Warnsignal**
- Marktkapitalisierung unter $1M → **Warnsignal**

### Schritt 2: Social Media & Influencer-Recherche
Suche nach:
- `[COINNAME] instagram promoted` / `[COINNAME] tiktok`
- `[INFLUENCER NAME] [COINNAME]` falls ein Promoter genannt wurde
- `[COINNAME] twitter pump`
- `[INFLUENCER NAME] crypto scam` oder `[INFLUENCER NAME] paid promotion`

**Zu bewertende Faktoren:**
- Wird der Coin von bezahlten Influencern ohne #ad-Kennzeichnung beworben?
- Handelt es sich um "Call-Gruppen" auf Telegram/Discord?
- Gibt es Berichte über den Influencer als Scammer?
- Koordinierte Hype-Posts ohne fundamentalen Inhalt?

### Schritt 3: Tokenomics (via Web Search)
Suche nach:
- `[COINNAME] tokenomics distribution`
- `[COINNAME] top holders percentage`
- `[COINNAME] liquidity locked`
- `[COINNAME] audit CertiK`

**Warnsignale (alles via öffentliche Quellen/CMC):**
- Top 10 Wallets halten > 50% des Supply → **kritisch**
- Keine veröffentlichten Tokenomics → **Warnsignal**
- Keine Audit durch bekannte Firma (CertiK, Hacken etc.) → **Warnsignal**
- 100% Tokens bereits im Umlauf beim Launch → **Warnsignal**

### Schritt 4: News & Community-Sentiment
Suche nach:
- `[COINNAME] scam review`
- `[COINNAME] reddit` 
- `[COINNAME] rugpull warning`

---

## Score-Berechnung

Bewerte jede Kategorie mit Punkten (je höher = mehr Risiko):

### Kategorie A: Projekt-Transparenz (max. 25 Punkte)
| Signal | Punkte |
|--------|--------|
| Anonymes Team, kein Doxxing | +10 |
| Kein Whitepaper | +8 |
| Kein Audit | +5 |
| Domain < 1 Jahr alt | +2 |

### Kategorie B: Tokenomics & On-Chain (max. 30 Punkte)
| Signal | Punkte |
|--------|--------|
| Liquidität nicht gelockt | +15 |
| Top 10 Wallets > 50% Supply | +10 |
| Dev kann Supply manipulieren (Mint-Funktion) | +5 |

### Kategorie C: Markt-Manipulation (max. 25 Punkte)
| Signal | Punkte |
|--------|--------|
| Volume/MCap Ratio > 200% | +10 |
| Volume/MCap Ratio 100-200% | +5 |
| Coin < 7 Tage alt | +8 |
| Coin 7-30 Tage alt | +4 |
| Plötzliche Preis-Spikes > 500% | +7 |

### Kategorie D: Influencer & Marketing (max. 20 Punkte)
| Signal | Punkte |
|--------|--------|
| Bekannte Scam-Influencer promoten den Coin | +10 |
| Bezahlte Werbung ohne Disclosure | +5 |
| Koordinierte Pump-Kampagnen auf Social Media | +5 |

---

## Ampel-System & Score-Interpretation

```
0-20 Punkte  → 🟢 GRÜN  – Relativ geringes Risiko (normale DYOR-Vorsicht)
21-40 Punkte → 🟡 GELB  – Erhöhtes Risiko, starke Vorsicht geboten
41-60 Punkte → 🟠 ORANGE – Hohes Risiko, sehr wahrscheinlich manipuliert
61-100 Punkte→ 🔴 ROT   – EXTREM HOHES RUGPULL-RISIKO
```

---

## Output-Format

Präsentiere den Report immer in diesem Format:

```
## 🔍 Rugpull-Analyse: [COINNAME]

### 🎯 Rugpull-Score: [X]/100 [AMPEL-EMOJI]
**[Risikostufe in einem Satz — z.B. "Sehr hohes Betrugsrisiko, mehrere kritische Signale gefunden."]**

---

### 📊 Score-Aufschlüsselung

**🏗️ Anonymität & Team** — [X]/25
[2-3 Sätze: Was wurde gefunden? Team doxxed? Whitepaper? Wer steckt dahinter?]

**💰 Tokenomics** — [X]/30
[2-3 Sätze: Wie ist die Verteilung? Audit vorhanden? Liquidität gesichert?]

**📈 Marktverhalten & Volatilität** — [X]/25
[2-3 Sätze: Volumen/MCap-Ratio, Preisentwicklung, Pump-Muster erkennbar?]

**📣 Influencer & Werbung** — [X]/20
[2-3 Sätze: Wer wirbt? Gibt es Disclosure? Bekannte Scammer involviert?]

---

### ⚠️ Die 3 größten Warnsignale
1. 🔴 [Kritischstes Signal + kurze Erklärung]
2. 🟠 [Zweites Signal + kurze Erklärung]
3. 🟡 [Drittes Signal + kurze Erklärung]

### 💡 Fazit
[3-4 Sätze: Gesamtbild, warum dieser Score, was bedeutet das für den User?]

⚖️ *Keine Finanzberatung. DYOR. Krypto ist hochspekulativ.*
```

---

## Wichtige Hinweise

- **Sei konservativ**: Im Zweifel lieber höher bewerten als zu niedrig — das schützt den Nutzer
- **Belege zitieren**: Bei jedem Warnsignal möglichst eine Quelle/URL nennen
- **Fehlende Daten**: Wenn Daten nicht gefunden werden können, ist das selbst ein Warnsignal (+3 Punkte für "keine verifizierbaren Infos")
- **Influencer-Gewichtung**: Wenn ein explizit genannter Influencer bekannte Scam-Geschichte hat, erhöhe den Marketing-Score entsprechend
- **Sprache**: Antworte in der Sprache des Nutzers (Deutsch wenn auf Deutsch gefragt)

---

## Beispiel-Coins für Orientierung

**Hohes Risiko (Referenz):** FOFAR, SafeMoon (2021), Squid Game Token
**Mittleres Risiko:** Neue Meme-Coins ohne Audit aber mit kleiner Community
**Geringes Risiko:** Etablierte Tokens mit CertiK-Audit, aktiver Entwicklung, transparentem Team
