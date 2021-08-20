# Investment Return Rate Estimation

I was trying to look for an investment return rate calculation tool online to estimate my investments, however I couldn't find one that would satisfy my need. Therefore this utility calculation tool was derived and implemented. 

## Problem Scope

This investment return rate calculation tool estimates the monthly and annual return rate of investments with an initial lumpsum and equal amount monthly installments. 

*Parameters*
 - Initial lumpsum investment: a_0
 - Monthly incremental investment: a_1
 - Current number of months of investment: n
 - Current cumulative value of invetment: b
 - Estimated Monthly Return Rate (EMRR): r
 - Estimated Annual Return Rate (EARR): R

*Definitions*
 - investment return rate (IRR)
 ```math
\text{IRR} = \frac{\text{cumulative amount after investment}}{cumulative amount before investment}
 ```

*Assumptions*
 - A homogeneous return rate was estimated, by ignoring shorter-term (less than monthly) up and down fluctuations;
 - A single value of monthly return rate was assumed - the monthly return rate variabilities were not considered in version 0.x;
 - EARR is eestimated by EMRR;
 - Cumulative amounts are obtained from the beginning of last investment, i.e. if you are estimating the IRR based on the cumulative ammounts obtained at the end of the last monthly investment, you'll need to minus the month numbers by 1. Zum Beispiel, I invested 1k every month since 1st Jan 2020, by 1st March 2020, I have invested 3k in total, but the March investment 1k has had no return yet. In case end of monthly investment estimations are used, simply deduct a single month installment. (rephrase - too complicated for non-tech audience)

## Solution
Equal amount of monthly installments with a same monthly IRR makes a geometric series. The problem can be framed into solving the following equation:

```math
a_0 * r^{n-1} + \frac{a_1 * (1 - r^n)}{1 - r} = b
```

### Numerical solution for the high-order equation

Newton-Raphson's method in solving the above high-order equation for the monthly IRR:

