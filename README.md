# Embedded Loan Prepayment Option Valuation using Longstaff-Schwartz Monte Carlo

## Overview

This project demonstrates the valuation of an embedded borrower prepayment option contained within an amortizing floating-rate loan.

Many lending agreements grant borrowers the right to repay or refinance debt before contractual maturity. Such rights create embedded optionality whose value depends on future market conditions, refinancing spreads, and optimal exercise decisions.

This repository presents a Python implementation of a valuation framework that combines:

- Monte Carlo simulation
- Mean-reverting credit spread modeling
- Longstaff-Schwartz Least Squares Monte Carlo (LSMC)
- Discounted Cash Flow (DCF) valuation

The project serves as an educational demonstration of derivative valuation and quantitative finance techniques.

---

## Financial Background

Corporate debt instruments often contain contractual provisions that allow borrowers to repay outstanding balances before maturity.

When market spreads decline below the contractual financing spread, borrowers may refinance at a lower cost. The resulting financing-cost savings create value for the borrower and represent an embedded option.

Unlike European-style options, refinancing decisions can generally be made at multiple dates throughout the life of the loan. This makes the problem analogous to valuing an American-style option.

---

## Valuation Objective

The objective of the model is to estimate the present value of future refinancing opportunities under uncertain market conditions.

The valuation answers the following question:

> What is the fair value today of the flexibility to refinance an existing loan if future market spreads evolve randomly through time?

---

## Methodology

### 1. Loan Cash Flow Projection

The model projects future outstanding balances and financing costs over the remaining life of the loan.

### 2. Credit Spread Simulation

Future refinancing spreads are simulated using a mean-reverting stochastic process:

\[
dS_t = \kappa(\theta - S_t)dt + \sigma dW_t
\]

where:

- \(S_t\) = refinancing spread
- \(\kappa\) = mean reversion speed
- \(\theta\) = long-term average spread
- \(\sigma\) = spread volatility
- \(W_t\) = Wiener process

### 3. Longstaff-Schwartz Least Squares Monte Carlo

At each potential exercise date, the model compares:

- Immediate refinancing value
- Expected continuation value

Continuation values are estimated using polynomial regression on simulated paths.

The borrower is assumed to refinance whenever:

\[
Exercise\ Value > Continuation\ Value
\]

### 4. Discounting

Optimal refinancing benefits are discounted to present value and averaged across simulation paths.

---

## Technical Implementation

### Core Components

- Spread simulation engine
- Loan cash flow generator
- Longstaff-Schwartz regression framework
- Exercise decision logic
- Discounting framework
- Monte Carlo aggregation

---

## Example Model Flow

```text
Loan Parameters
        │
        ▼
Spread Simulation
        │
        ▼
Exercise Value Calculation
        │
        ▼
Longstaff-Schwartz Regression
        │
        ▼
Optimal Exercise Decision
        │
        ▼
Discount Future Payoffs
        │
        ▼
Estimated Option Value
```

---

## Example Assumptions

The repository uses synthetic values for demonstration purposes:

| Parameter | Example Value |
|-----------|--------------|
| Loan Balance | €100 million |
| Loan Term | 3 years |
| Contractual Margin | 2.50% |
| Initial Market Spread | 1.00% |
| Mean Reversion | 0.05 |
| Volatility | 0.50% |
| Risk-Free Rate | 2.50% |
| Monte Carlo Paths | 10,000 |

These assumptions are illustrative only and do not correspond to any real transaction.


---

## Key Learning Outcomes

This project demonstrates practical applications of:

- Quantitative finance
- Financial engineering
- Derivative valuation
- Stochastic processes
- Monte Carlo simulation
- Python-based financial modeling
- Risk analytics
- IFRS 9 valuation concepts

---

## Potential Enhancements

Future improvements may include:

- Hull-White interest rate models
- Multi-factor spread dynamics
- Credit curve calibration
- Scenario stress testing
- Sensitivity analysis dashboards
- Parallel computing for large simulations
- IFRS 13 fair value reporting outputs

---

## Performance Considerations

The current implementation prioritizes:

- Transparency
- Reproducibility
- Auditability
- Educational value

Commercial valuation systems would typically incorporate:

- Market data integration
- Calibration frameworks
- Multi-factor models
- Validation controls
- Production-grade performance optimization

---

## Disclaimer

This repository is provided for educational and portfolio purposes only.

All datasets, assumptions, loan schedules, valuation results, market parameters, and examples are synthetic or anonymized. No confidential information, proprietary methodologies, client data, employer data, or third-party intellectual property are included in this repository.

The model should not be used for investment, accounting, risk management, regulatory, or valuation purposes without independent validation.
