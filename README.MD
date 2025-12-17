# Trading Strategy Backtests

Backtests mehrerer Intraday-Trading-Strategien auf **15 Jahren NQ1! 1‑Minute-Daten** (ca. **5 Millionen Candles**).


***

## Table of Contents

- [Overview](#overview)  
- [Data](#data)  
- [Installation](#installation)  
- [Usage](#usage)  
- [Strategy 1 – Bollinger Bands Arbitrage](#strategy-1--bollinger-bands-arbitrage)  
- [Strategy 2 – Rolling Directional Squeeze and Reversal](#strategy-2--rolling-directional-squeeze-and-reversal)  
- [License](#license)

***

## Overview

Dieses Repository enthält Research-Code und Backtests für systematische NQ1!-Strategien mit Fokus auf Mean Reversion, Volatilitätsregime und Squeezes. Ziel ist es, robuste regelbasierte Intraday-Setups quantitativ zu evaluieren.

***

## Data

- Underlying: NQ1! (E-mini Nasdaq 100 Front Month Future)  
- Timeframe: 1‑Minute OHLCV  
- History: ~15 Jahre, ca. 5M Candles (Rohdaten nicht im Repo enthalten)

***

## Installation

```bash
git clone https://github.com/<your-username>/<your-repo>.git
cd <your-repo>
pip install -r requirements.txt
```

**Core dependencies:**

```text
pandas
numpy
matplotlib
plotly
```

***

## Usage

Typischer Workflow:

```bash
# Beispiel: Strategy 1 Backtest
python backtest_bb_arbitrage.py --start 2010-01-01 --end 2025-01-01

# Beispiel: Strategy 2 Backtest
python backtest_directional_squeeze.py --start 2010-01-01 --end 2025-01-01
```

Backtest‑Ergebnisse (Equity Curve, Drawdown, Kennzahlen) werden als Plots und CSVs im `results/`‑Ordner gespeichert.

***

## Strategy 1 – Bollinger Bands Arbitrage

**Assumptions**

- Der Markt wechselt dynamisch zwischen Regimen (Volatilität, Trendstärke).  
- Preis bewegt sich wellenförmig um seinen Mittelwert und oszilliert um eine mittlere Reversion.

**Concept**

- Preis folgt einem zyklischen Prozess: Deviation → Reversion → Squeeze → neue Deviation.  
- Entries erfolgen während des Squeezes, da anschließend typischerweise eine Expansion/Deviation folgt.  
- Trendstärke und Dauer sind unbekannt, daher werden keine Tops/Böden gefadet, sondern stabile Deviations nach einer Phase der Stabilisierung gehandelt.  
- Annahme: Nachdem Buyside-Liquidität geholt wurde, wird mittelfristig auch Sellside-Liquidität angegriffen (und umgekehrt).  
- Targets sind trend- und volatilitätsadjustiert; Bollinger Bänder passen sich dynamisch an.  
- Es wird kein klassischer Stop-Loss verwendet, das Risikomanagement erfolgt über Positionsgrößen, Volatilität und Regelwerk.

***

## Strategy 2 – Rolling Directional Squeeze and Reversal

**Assumptions**

- Preisverläufe ähneln einer Achterbahn: Je weiter eine Bewegung läuft, desto stärker wirkt „Gravitation“ (Momentum-Exhaustion).  
- Wie in Strategy 1 wird der Markt als Summe aus Trendkomponente und einer schwankenden, verrauschten Sinusfunktion modelliert.

**Concept**

- Wenn Momentum abnimmt und die Expansion an Kraft verliert, neigt der Preis dazu, zu vorherigen Pivots zu revertieren.  
- Diese Reversionen füllen Ineffizienzen und führen kurzfristig zu einer Stabilisierung der Marktstruktur.

***