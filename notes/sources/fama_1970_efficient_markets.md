# Fama (1970) - Efficient Capital Markets

## Reference
**Citation key**: @fama1970efficientmarkets
**Authors**: Fama, Eugene F.
**Year**: 1970
**Title**: Efficient Capital Markets: A Review of Theory and Empirical Work

## Abstract

This paper reviews theoretical and empirical literature on the efficient markets model, which posits that **security prices at any time "fully reflect" all available information**.
The paper examines three levels of market efficiency: **weak** form (prices reflect historical price information), **semi-strong** form (prices reflect all publicly available information), and **strong** form (prices reflect all information, including private information).
The evidence strongly supports the weak and semi-strong forms, with limited contradictions to the strong form.

--- 

## Key Definitions

**Efficient Market**: A market in which prices always "fully reflect" available information. The primary role is allocation of ownership of the economy's capital stock, where prices provide accurate signals for resource allocation.

**Three Forms of Market Efficiency**:
1. **Weak Form**: Information subset includes only historical prices
2. **Semi-Strong Form**: Information subset includes all obviously publicly available information
3. **Strong Form**: Information subset includes all information relevant for price formation, including monopolistic information

## Important Results/Ideas

### The Expected Returns (Fair Game) Model
* Market equilibrium conditions can be stated in terms of expected returns
* For security j: E(p̃ⱼ,ₜ₊₁|Φₜ) = [1 + E(r̃ⱼ,ₜ₊₁|Φₜ)]pⱼₜ
* Implies that trading systems based only on information in Φₜ cannot have expected profits in excess of equilibrium expected returns
* The excess return zⱼ,ₜ₊₁ = r̃ⱼ,ₜ₊₁ - E(r̃ⱼ,ₜ₊₁|Φₜ) is a "fair game": E(zⱼ,ₜ₊₁|Φₜ) = 0
* Serial covariances of a fair game variable are zero (linearly independent observations)

### The Submartingale Model
* Special case where E(p̃ⱼ,ₜ₊₁|Φₜ) ≥ pⱼₜ (expected returns are non-negative)
* Implies that "one security and cash" mechanical trading rules cannot outperform buy-and-hold strategy
* Important for testing profitability of trading systems

### The Random Walk Model
* Strongest assumption: successive returns are independent and identically distributed
* f(r̃ⱼ,ₜ₊₁|Φₜ) = f(r̃ⱼ,ₜ₊₁)
* Goes beyond fair game model by requiring entire distribution to be independent of past information
* Best viewed as special case arising when environmental conditions cause return distributions to repeat through time

### Weak Form Test Results
* **Serial Correlation Tests**: Absolute correlations always close to zero (Table 1 shows coefficients rarely exceeding 0.10)
* **Filter Tests** (Alexander; Fama-Blume): Very small filters (≤1.5%) show slight profitability but cannot overcome even minimum transaction costs
* **Evidence of slight positive dependence** in daily returns, but insufficient for profitable trading after costs
* **Random walk largely supported** for returns covering a day or longer
* **Niederhoffer-Osborne findings**: Excessive reversals in transaction-to-transaction prices due to market structure (limit orders), not exploitable for profits

### Semi-Strong Form Test Results
* **Stock Splits** (FFJR): Market correctly anticipates dividend implications; prices adjust by split month with no subsequent drift
* **Earnings Announcements** (Ball-Brown): 85-90% of information anticipated before announcement month
* **Discount Rate Changes** (Waud): Small announcement effects (<0.5%), with some anticipation
* **Secondary Offerings** (Scholes): Price declines of 1-2% reflect negative information, not selling pressure; adjustment complete by offering date
* **Conclusion**: Prices efficiently adjust to public information

### Strong Form Test Results
* **Mutual Fund Performance** (Jensen): 115 funds studied 1955-64
  - 89 of 115 funds underperformed market line (net of all costs)
  - Average underperformance of 14.6% over 10 years
  - Even gross of expenses, average deviation only 0.09%
  - No evidence of persistent superior performance by individual funds
  - Conclusion: Fund managers have no special information or forecasting ability
* **Documented Exceptions**:
  - NYSE specialists profit from monopolistic access to limit order book
  - Corporate insiders have monopolistic access to firm information
* **General Conclusion**: Only specialists and insiders show monopolistic information access; no evidence for broader investment community

### Market Model Results
* rⱼ,ₜ₊₁ = αⱼ + βⱼrₘ,ₜ₊₁ + uⱼ,ₜ₊₁ is well-specified
* Parameters stable over time (Blume: post-WWII period)
* Consistent with Sharpe-Lintner CAPM framework
* King: ~50% of individual stock variance explained by market factor, ~10% by industry factors

### Distributional Evidence
* Mandelbrot-Fama: Returns better described by non-normal stable distributions (fat tails) than normal distribution
* Important for statistical testing procedures and interpretation
* Roll: Treasury Bills also exhibit non-normal stable distributions

## Quotes

> "In an efficient market, prices 'fully reflect' available information in the sense that the process of price formation must be specified such that equilibrium expected returns are formed on the basis of available information."

> "The evidence in support of the efficient markets model is extensive, and (somewhat uniquely in economics) contradictory evidence is sparse."

> "For the purposes of most investors the efficient markets model seems a good first (and second) approximation to reality."

## Personal Notes
