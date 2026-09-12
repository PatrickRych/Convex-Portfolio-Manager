# Methodology

This document summarizes the main quantitative ideas represented in the CONVEX project. The public workbook is a demonstration implementation; the larger private workbook contains additional logic and production-specific rules.

## 1. Signed option-leg exposure

Each option leg is assigned a signed quantity:

- long leg: positive quantity
- short leg: negative quantity

For a standard U.S. equity option multiplier of 100:

```text
Net Delta = Option Delta × Signed Contracts × 100
Net Theta = Option Theta × Signed Contracts × 100
Net Vega  = Option Vega  × Signed Contracts × 100
Net Gamma = Option Gamma × Signed Contracts × 100
```

This creates a consistent base for aggregating multi-leg positions.

## 2. Dollar delta

Position directional exposure is translated into dollars using the underlying spot price:

```text
Dollar Delta = Net Delta × Underlying Price
```

The private model also calculates a SPY-equivalent approximation using beta:

```text
Beta-Adjusted Dollar Delta = Dollar Delta × Beta_vs_SPY
```

This allows positions across different underlyings to be viewed on a common directional scale.

## 3. Realized volatility

The private model calculates annualized realized volatility from daily returns. One version adjusts the historical lookback to the option's remaining DTE, subject to minimum / maximum windows.

Conceptually:

```text
RV = stdev(daily returns over lookback) × sqrt(annualization factor)
```

The purpose is to compare the option's volatility pricing with what the underlying has recently realized.

## 4. Implied-versus-realized volatility

One private-model measure expresses the variance-risk-premium relationship as:

```text
VRP ratio = IV / RV - 1
```

Positive values indicate implied volatility above realized volatility; negative values indicate implied volatility below realized volatility. It is a relative-volatility diagnostic, not a forecast guarantee.

## 5. Probability of profit approximation

For structures with an explicit breakeven, the private workbook uses a lognormal distribution approximation based on:

- spot price
- breakeven
- volatility
- time to expiry

This is used as a decision input rather than a standalone trading signal.

## 6. Trend and volatility state

The model combines several forms of market-state information:

- moving-average trend classification
- ATR / standardized ATR measures
- realized-volatility rank
- implied-volatility rank / percentile inputs
- implied-versus-realized volatility

The goal is to characterize whether the position is operating in a low-, normal-, rich-, or shifting-volatility environment and whether price trend is supportive or deteriorating.

## 7. Volatility-targeted deployment

A private-model deployment rule scales target utilization inversely with volatility:

```text
Target Utilization = Base Utilization × (Volatility Anchor / Current Volatility)^k
```

The result is bounded by configurable minimum and maximum utilization levels.

Interpretation:

- higher volatility → lower target deployment
- lower volatility → higher allowable deployment

This is a risk-scaling framework, not a prediction model.

## 8. Factor exposure and risk contribution

Positions carry manually assigned factor / theme labels. Portfolio aggregation then summarizes position count, premium, delta, beta-adjusted delta, theta, vega, notional, volatility, and other metrics by factor.

A simple risk-contribution view combines capital at risk with volatility to identify areas where concentration and volatility overlap.

## 9. Derisking priority

The private workbook contains a cut-ranking framework that attempts to convert a portfolio-level requirement such as "reduce exposure" into an ordered position list.

Inputs include measures such as:

- premium / capital held
- probability-of-profit estimate
- factor concentration

The ranking is intended to prioritize inefficient or concentrated risk rather than cut positions arbitrarily.

## 10. Risk limits

The portfolio dashboard normalizes several metrics against warning and breach thresholds. Examples include:

- buying-power utilization
- directional exposure relative to equity
- beta-adjusted directional exposure
- volatility exposure
- theta exposure
- position count
- factor concentration

Some thresholds in the private workbook are explicitly uncalibrated and should be treated as provisional risk-policy inputs rather than empirical findings.

## 11. Scenario analysis

The Scenario Lab is designed to reprice positions across a grid of:

- price moves
- time decay
- volatility shifts

This is preferable to assuming that current Greeks remain constant over a large shock. The current implementation is still simplified relative to a full volatility-surface / American-option model.

## 12. Position sizing

The project includes fractional Kelly logic based on observed win rate and payoff ratio, then reduces the full Kelly result by a configurable divisor and applies qualitative grade multipliers.

This should be interpreted cautiously because pooled historical trades may represent heterogeneous strategies with different payoff distributions.
