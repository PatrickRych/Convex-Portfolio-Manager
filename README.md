# CONVEX Portfolio Manager

**Options portfolio risk and decision-support system built from a discretionary trading workflow.**

> **Portfolio project:** CONVEX began as a private Excel-based portfolio-management system designed to translate option positions into leg-level Greeks, position analytics, portfolio exposures, risk limits, scenario analysis, and management signals. This repository contains a **public synthetic demonstration workbook** using a fictional **$100,000 portfolio**. All positions, account values, and performance figures shown here are synthetic and are included only to demonstrate the system's functionality.

![CONVEX Risk Manager](risk-manager.png)

## Why I built it

Broker platforms are good at showing positions and P&L, but I wanted a framework that answered different questions:

- What am I actually exposed to after decomposing multi-leg positions?
- How much directional, volatility, theta, gamma, factor, and concentration risk is in the book?
- Which positions are consuming risk inefficiently?
- When should a position be held, rolled, trimmed, overlaid, or closed?
- How should portfolio deployment change as volatility changes?

CONVEX was built to turn those questions into a repeatable analytical workflow.
##
### 📥 Download the Working Excel Demo

**[Download CONVEX Portfolio Manager — Excel Demo](CONVEX_Portfolio_Manager_Demo.xlsx)**

Explore the synthetic $100,000 portfolio, modify inputs, and inspect the quantitative risk models.

### 📖 Operating Guide & Methodology

**[Read the CONVEX Operating Guide (PDF)](CONVEX_Portfolio_Manager_Operating_Guide.pdf)**

A detailed walkthrough of how I use CONVEX, including trade entry, position analysis, options Greeks, portfolio risk calculations, quantitative formulas, scenario analysis, and position-management decisions.
##

## System architecture

```mermaid
flowchart LR
    A[Options Journal<br/>trade system of record] --> B[Positional Analysis<br/>position master]
    G[Market Data<br/>price, RVOL, ATR, beta, correlation] --> B
    B --> C[Risk View<br/>leg decomposition + Greeks]
    H[Options Data<br/>private model: Options Samurai<br/>public demo: synthetic inputs] --> C
    C --> B
    F[Event Dashboard<br/>catalyst awareness] --> B
    B --> D[Risk Manager<br/>portfolio aggregation]
    B --> E[Scenario Lab<br/>what-if analysis]
    C --> E
    D --> I[Decision Outputs<br/>limits, sizing, hedging, derisking]
```

The original model contains a deliberate two-way dependency between **Positional Analysis** and **Risk View**: position identity and structure flow down to the leg engine, while leg-level prices and Greeks flow back up for position and portfolio aggregation.

## Core workflow

1. **Record the trade** in the journal.
2. **Select the live book** and classify each position.
3. **Explode multi-leg structures** into individual option legs.
4. **Attach pricing and Greeks** to each leg.
5. **Aggregate leg risk** back to the position level.
6. **Calculate position analytics** including volatility, probability, trend, premium efficiency, and management levels.
7. **Aggregate the portfolio** into directional, volatility, factor, concentration, margin, and sizing views.
8. **Generate decision support** such as `OK`, `CAUTION`, `WARNING`, `ROLL`, `OVERLAY`, `CLOSE`, and derisking priorities.

## Synthetic demonstration views

The screenshots below come from the public demonstration copy of CONVEX. **Every position, account value, and performance figure shown is fictional. No live account data or actual investment performance is presented.**

### Position analytics

![Positional Analysis](positional-analysis.png)

The position layer combines trade structure, DTE, P&L, volatility state, momentum/trend measures, skew/IV information, Greeks, portfolio factor tags, management levels, and rule-based action outputs.

### Leg decomposition and Greek aggregation

![Risk View](risk-view.png)

Risk View converts position-level option structures into individual legs, applies signed quantities, attaches option Greeks, and aggregates the results into ticker- and portfolio-level exposure measures.

### Event awareness

![Event Dashboard](event-dashboard.png)

The event dashboard maintains a forward calendar of macro, options-expiration, volatility, and portfolio-review events. Event proximity can feed back into position-management rules.

### Synthetic historical trade analytics

![Historical Performance](historical-performance.png)

The historical-performance view is populated with **synthetic closed trades** solely to demonstrate how the framework evaluates results by strategy, structure, DTE, and time utilized. It is **not a live or claimed investment track record**.

<details>
<summary>Additional demo screenshots</summary>

### Trade journal

![Trade Journal](trade-journal.png)

### Scenario lab

![Scenario Lab](scenario-lab.png)

</details>

## Quantitative components

The larger implementation includes:

- multi-leg option ticket parsing and signed-leg construction
- delta, theta, vega, and gamma aggregation
- dollar delta and beta-adjusted dollar delta
- DTE-matched realized volatility
- ATR and standardized volatility/trend measures
- beta and correlation versus SPY
- implied-versus-realized volatility measures
- probability-of-profit approximation
- volatility-regime classification
- volatility-targeted deployment
- inverse-volatility factor sizing
- concentration and factor exposure analysis
- rule-based position management
- derisking / cut-list prioritization
- portfolio stress scenarios
- fractional Kelly-based position sizing
- Black-Scholes scenario repricing

See [`methodology.md`](methodology.md) for the methodology overview.

## Working demo

The downloadable workbook is here:

**[`CONVEX_Portfolio_Manager_Demo.xlsx`](CONVEX_Portfolio_Manager_Demo.xlsx)**

The workbook uses a **synthetic $100,000 portfolio** so it can be shared publicly without exposing brokerage information, live trades, or licensed third-party market data. It demonstrates the production-style workflow and analytical logic.

## Data sources

The private workbook uses Microsoft Excel market-data functionality for underlying price history and, where available, **Options Samurai** for option-level pricing, Greeks, implied volatility, and related option statistics.

Those vendor values are **not redistributed in this repository**. The public demo uses synthetic/demo inputs.

## What this project demonstrates

This project is intended to demonstrate my ability to:

- translate a trading process into a structured analytical system
- connect transaction-level data to position- and portfolio-level risk
- design quantitative decision rules rather than rely only on visual dashboards
- work with option Greeks and multi-leg structures
- build auditable models in Excel using dynamic arrays and formula-driven logic
- identify model limitations and data-quality risks
- communicate a complex analytical workflow clearly

I built CONVEX as a **self-directed project**. It should not be interpreted as institutional software, audited risk infrastructure, or investment advice.

## Known limitations

- the public workbook uses synthetic rather than live option data
- some management thresholds are research hypotheses / practitioner rules rather than statistically validated findings
- the production stress framework is simplified relative to a full nonlinear portfolio simulation
- the current implementation is Excel-first and contains logic that would be easier to test and version-control in Python
- the private model relies on external data availability

A fuller discussion is available in [`limitations.md`](limitations.md).

## Next development stage

The natural next step is to move selected engines from spreadsheet formulas into Python, beginning with:

1. multi-leg structure parsing
2. pricing and Greek calculations
3. rolling realized-volatility statistics
4. portfolio exposure aggregation and limits
5. point-in-time state storage for reproducible testing

That would create a progression from **spreadsheet prototype → documented model → testable analytics code → interactive application**.

## Repository structure

```text
Convex-Portfolio-Manager/
├── README.md
├── CONVEX_Portfolio_Manager_Demo.xlsx
├── architecture.md
├── methodology.md
├── limitations.md
├── risk-manager.png
├── risk-view.png
├── positional-analysis.png
├── event-dashboard.png
├── historical-performance.png
├── trade-journal.png
├── scenario-lab.png
└── .gitignore
```

---

**Disclaimer:** This repository is an analytical portfolio project for demonstration and research purposes only. All displayed portfolio and performance data are synthetic. It is not financial advice, a recommendation to trade, or a production risk-management system.
