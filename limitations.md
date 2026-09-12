# Limitations and Model-Risk Notes

A major goal of this repository is to present the project transparently rather than imply a level of precision the model does not have.

## Public demo limitations

- All portfolio, option, and market values in the downloadable workbook are synthetic.
- The demo is smaller than the private production workbook and does not replicate every feature one-for-one.
- It is intended to demonstrate workflow, formulas, and system design—not produce live trading recommendations.
- Third-party option data has been removed from the public version.

## Private-model limitations

The larger Excel implementation has several known limitations that motivate future development.

### Spreadsheet architecture

The production workbook is formula-heavy and contains mutually dependent analytical sheets. This makes refactoring, testing, and version control harder than it would be in a software-based implementation.

### Capacity and input fragility

Some production ranges are fixed-size and some option structures are parsed from formatted text. Poorly formatted inputs can therefore create silent omissions or misclassification unless additional validation is added.

### External-data dependence

The private model relies on Excel market-data functionality and external option analytics. Data outages, stale values, or ticker mismatches can propagate into risk outputs.

### Simplified option modelling

Some local calculations use Black-Scholes-style assumptions that do not fully model:

- American exercise
- dividends
- borrow / hard-to-borrow effects
- the full volatility surface
- volatility-of-volatility

### Stress testing

The portfolio stress framework is simpler than a full nonlinear portfolio simulation. A production-quality implementation should incorporate gamma, skew changes, cross-asset correlation changes, and potentially full repricing under multiple state variables.

### Beta and correlation

Single-factor beta / correlation versus SPY is a useful translation tool but can become unstable during stressed markets. It should not be interpreted as a structural hedge ratio.

### Threshold calibration

Several management and risk thresholds originated as practitioner rules or hypotheses. They are not all supported by formal out-of-sample validation. A future research layer should test them point-in-time and by strategy type.

### Performance statistics

Pooling trades across materially different strategies can distort win rate, payoff ratio, Kelly sizing, and related performance metrics. Strategy-specific distributions are preferable.

### Point-in-time reproducibility

A spreadsheet that continually refreshes `TODAY()`, market data, percentiles, and state variables does not automatically preserve historical model states. Proper backtesting requires point-in-time snapshots rather than reconstructing the past using today's calculations.

## Planned improvements

The highest-value future improvements are:

1. Python-based option-leg parser with unit tests
2. independent pricing / Greek engine
3. pandas-based rolling market statistics
4. persistent point-in-time data store
5. reconciliation tests between leg, position, factor, and portfolio totals
6. nonlinear portfolio scenario engine
7. strategy-specific performance and sizing models
8. interactive web application layer

These limitations are part of the reason this project is useful as a portfolio piece: it demonstrates not only model construction, but also model-risk awareness and the ability to identify where a spreadsheet prototype should evolve into testable software.
