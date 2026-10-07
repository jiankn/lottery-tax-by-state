# Lottery tax by state (2026)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23202118.svg)](https://doi.org/10.5281/zenodo.23202118)

State and city tax on lottery winnings for all 50 states, Washington, D.C., New York City and Yonkers, in one CSV and one JSON file. Each row has the 2026 top income tax rate, whether the state taxes lottery prizes, the lottery withholding rate where the state publishes one, a link to the official source, and the take-home on a $1,000,000 prize.

The data comes from [Jackpot Calculator](https://jackpotcalculator.com/), where the same figures power a lottery tax calculator for any prize and state. The [lottery tax by state table](https://jackpotcalculator.com/lottery-tax-by-state/) shows them with explanations.

## Files

| File | Contents |
|---|---|
| `data/lottery-tax-by-state-2026.csv` | 53 rows: 50 states, D.C., New York City, Yonkers |
| `data/lottery-tax-by-state-2026.json` | Same rows, plus metadata, assumptions and the full federal, state and city brackets (`rules`) needed to reproduce every figure |

## Notebook

[`notebooks/powerball-lump-sum-vs-annuity.ipynb`](notebooks/powerball-lump-sum-vs-annuity.ipynb) uses the full brackets in the JSON file to compare the Powerball lump sum and the 30-year annuity after taxes in every state: take-home, present value at different discount rates and the break-even rate. Its last cell checks the results against the [Powerball calculator](https://jackpotcalculator.com/powerball-calculator/) to the cent. [Open it in Colab](https://colab.research.google.com/github/jiankn/lottery-tax-by-state/blob/main/notebooks/powerball-lump-sum-vs-annuity.ipynb) to change the jackpot, filing status or other income.

## Columns

| Column | Meaning |
|---|---|
| `jurisdiction`, `code`, `level` | Name, postal code (or `NYC` / `YONKERS`), `state` or `city` |
| `sells_powerball`, `sells_mega_millions` | Whether the jurisdiction sells the game |
| `taxes_lottery_winnings` | `false` where lottery prizes are exempt from state income tax (California, and states with no income tax) |
| `top_rate_single`, `top_rate_starts_at_single`, `top_rate_joint` | Top 2026 income tax rate and the taxable income where it starts for a single filer, and the top rate for joint filers. Decimal: `0.0495` = 4.95% |
| `lottery_withholding_rate` | Rate the lottery withholds for state tax when a prize is claimed. **Left blank unless it was checked against an official source** |
| `withholding_threshold_usd` | Prize size where state withholding starts, where it differs from the federal $5,000 |
| `withholding_source`, `withholding_checked_on` | Official page for the withholding rate, and the date it was checked |
| `rates_source` | Source of the income tax brackets |
| `state_local_tax_on_1m`, `take_home_on_1m` | State and local tax on, and take-home from, a $1,000,000 lump sum (see assumptions) |
| `notes` | Maryland includes the average county tax; city rows include New York State tax |

## Assumptions

`take_home_on_1m` and `state_local_tax_on_1m` are for a $1,000,000 prize taken as a lump sum by a single filer with no other income who lives in the jurisdiction, using 2026 federal and state rates and the standard deduction. Federal income tax on that prize is $320,000 everywhere: 24% ($240,000) is withheld at claim and the rest is due at filing.

Not included: county and city income taxes outside New York City, Yonkers and the Maryland county average; tax for winners who bought the ticket in another state; deductions beyond the standard deduction. This is a summary of published rates, not tax advice.

## Updates

Rates are checked at the start of each tax year and every quarter. A new tax year gets a new file and a new release; corrections are listed in the release notes and in the [Jackpot Calculator methodology](https://jackpotcalculator.com/methodology/#changes).

## License and citation

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Credit "Jackpot Calculator" with a link to https://jackpotcalculator.com/lottery-tax-by-state/. Citation details are in [`CITATION.cff`](./CITATION.cff); each release is archived on Zenodo: [10.5281/zenodo.23202118](https://doi.org/10.5281/zenodo.23202118) (all versions).
