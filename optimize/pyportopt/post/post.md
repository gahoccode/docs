Here's the extracted page with all relevant methods, parameters, returns, return types, and math formulas:

---

# Post-processing weights

After optimal weights have been generated, it is often necessary to do some post-processing before they can be used practically. In particular, you are likely using portfolio optimization techniques to generate a **portfolio allocation** – a list of tickers and corresponding integer quantities that you could go and purchase at a broker.

PyPortfolioOpt offers two ways of solving this problem: one using a simple greedy algorithm, the other using integer programming.

## Greedy algorithm

`DiscreteAllocation.greedy_portfolio()` proceeds in two ‘rounds’. In the first round, we buy as many shares as we can for each asset without going over the desired weight. For example, if you want $1500 worth of Apple stock and Apple shares are $190 each, you'd buy 7 shares at a cost of $1330. 

In the second round, we address any deviation from the desired weights, buying additional shares of assets with the greatest discrepancy. This approach generally leaves minimal funds unallocated.

## Integer programming

This method treats the discrete allocation as an integer programming problem. The optimization problem can be expressed as:

\[ 
\begin{aligned}
& \underset{x \in \mathbb{Z}^n}{\text{minimize}} & & r + \lVert wT - x \odot p \rVert_1 \\
& \text{subject to} & & r + x \cdot p = T
\end{aligned}
\]

Where:
- \( T \in \mathbb{R} \) is the total dollar amount to be allocated.
- \( p \in \mathbb{R}^n \) is the array of the latest prices.
- \( w \in \mathbb{R}^n \) represents the set of target weights.
- \( x \in \mathbb{Z}^n \) is the integer allocation result.
- \( r \in \mathbb{R} \) is the remaining unallocated value.

## Dealing with shorts

As of v0.4, `DiscreteAllocation` handles shorts by finding separate discrete allocations for long-only and short-only sections of the portfolio. You can pass a short ratio, defaulting to 0.30 for a 130/30 long-short balance.

## Documentation reference

The `discrete_allocation` module contains the `DiscreteAllocation` class.

### Class: `DiscreteAllocation`

_Public methods:_
- `greedy_portfolio()`
- `lp_portfolio()`

_Public methods and parameters:_

- `greedy_portfolio(reinvest=False, verbose=False)`
  - **Parameters:**
    - **reinvest** (_bool_, defaults to False) – Whether to reinvest cash from shorting.
    - **verbose** (_bool_, defaults to False) – Print error analysis?
  - **Returns:**
    - Number of shares for each ticker that should be purchased and leftover funds.
  - **Return type:** (dict, float)

- `lp_portfolio(reinvest=False, verbose=False, solver='ECOS_BB')`
  - **Parameters:**
    - **reinvest** (_bool_, defaults to False) – Whether to reinvest cash from shorting.
    - **verbose** (_bool_) – Print error analysis?
    - **solver** (_str_, defaults to "ECOS_BB") – CVXPY solver to use.
  - **Returns:**
    - Number of shares for each ticker that should be purchased and leftover funds.
  - **Return type:** (dict, float)
