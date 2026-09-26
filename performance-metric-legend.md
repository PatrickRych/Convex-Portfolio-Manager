# 2026 Performance Review — Metric Legend

[← Back to the 2026 performance review](performance-review.md) · [← CONVEX Portfolio Manager](README.md)

These definitions explain the columns and abbreviations used in the 2026 CONVEX trading-performance review.

> **R convention used in this review:** R is **capital R** — realized Net P&L divided by estimated initial / maximum capital risk. It is not necessarily the same as planned-stop R, so R-based metrics should be interpreted as risk-normalized journal diagnostics rather than a perfect measure of intended trade risk.

## Core abbreviations

- **n** — Number of closed trades included in the strategy or setup sample.
- **PF — Profit Factor** — Gross winning dollars divided by the absolute value of gross losing dollars.
  - **PF > 1.0** — gross profits exceeded gross losses.
  - **PF = 1.0** — approximately breakeven before costs.
  - **PF < 1.0** — gross losses exceeded gross profits.
- **R** — Trade outcome expressed relative to the review's estimated capital risk.
  - Example: **+1.0R** means a profit equal to one unit of estimated risk; **-1.0R** means a loss equal to one unit.

## Strategy → Setup table

- **Strategy / Setup** — Broad trading strategy followed by the specific setup used inside that strategy.
- **Trades** — Total number of closed trades in that row.
- **Sample** — Visual sample-size indicator used to distinguish better-populated rows from small samples.
- **Win %** — Percentage of closed trades with positive realized P&L.
- **Net P&L $** — Total realized dollar profit or loss for the row.
- **Avg P&L $** — Average realized dollar profit or loss per trade.
- **Profit Factor** — Gross profits ÷ absolute gross losses.
- **Payoff** — Average winning trade ÷ absolute average losing trade.
  - Example: a payoff of **2.0** means the average winner was twice the size of the average loser.
- **Avg Winner $** — Average realized dollar P&L of winning trades only.
- **Avg Loser $** — Average realized dollar P&L of losing trades only.
- **Largest Loss $** — Largest single realized dollar loss in the row.
- **Avg R** — Arithmetic mean of the R-multiples for trades with an R value.
- **Median R** — Middle R outcome after the R-covered trades are ranked from worst to best.
  - Less sensitive to unusually large winners or losers than Avg R.
- **Total R** — Sum of all R-multiples in the row.
  - Example: +1R, -0.5R, +2R, -1R and +0.5R = **+2R Total R**.
- **R Expectancy** — Average risk-adjusted outcome per trade for the sample, expressed in R.
  - In this review it is the row-level expected R outcome based on the observed historical trade sample.
- **Avg Days Held** — Average number of calendar days a trade remained open.
- **% of Total P&L** — The row's contribution to total realized portfolio P&L.
  - Positive percentages added to portfolio profit; negative percentages detracted from it.

## Reading the metrics together

No single column establishes an edge by itself. A high **Win %** can coexist with weak **Payoff**, a strong **PF** can come from a small sample, and positive **Net P&L** can coexist with weak **Avg R** if sizing, missing-R trades or a few large winners dominate the dollar result. The review therefore uses these metrics together rather than ranking strategies on one number alone.

---

**Performance disclosure:** These definitions describe the supplied 2026 journal review. The performance figures are self-reported and unaudited and have not been reconciled to brokerage statements in this repository.
