[README.md](https://github.com/user-attachments/files/35444249/README.md)
# When to Invest: Brokerage vs Time in the Market

A free Excel calculator that answers one question: **if you save a fixed amount regularly and every share purchase costs a brokerage fee, how often should you actually buy?**

Buying every time you're paid gets your money invested sooner, but you pay the fee every time. Saving up and buying less often means fewer fees, but your money sits in a savings account earning less in the meantime. This workbook finds where that trade-off balances for your numbers.

## Example

Saving **$100 a week** for **20 years**, with an **$8** fee per trade, a **7%** expected yearly return on investments and **4%** interest on savings:

| | |
|---|---|
| Best strategy | Buy every **18 weeks** (about $1,800 per trade) |
| Value at the end | **$218,424** |
| Value if you bought every week | $202,777 |
| Difference | **$15,646** more by buying every 18 weeks |
| Brokerage paid | $456 (vs $8,320 buying weekly) |

The result is forgiving: anything from buying every 13 to every 23 weeks ends up within $100 of the best.

## How to use it

1. Download `When to Invest.xlsx` and open it in Microsoft Excel (it also calculates correctly in LibreOffice Calc).
2. On the **Calculator** tab, change the blue cells to your own numbers.
3. Read the answer under the green **OUTPUT STARTS HERE** banner.

### Inputs

| Input | What it means |
|---|---|
| Amount you save each period | e.g. how much you set aside each pay |
| Periods per year | 52 = weekly, 26 = fortnightly, 12 = monthly |
| Expected yearly return on investments | Your assumption for the long-run average, including reinvested dividends. Not a forecast. |
| Yearly interest on savings | What your savings account pays while the money waits to be invested |
| Brokerage: fixed fee per trade | e.g. $8 |
| Brokerage: percentage of each trade | Leave at 0% for a flat fee. A percentage fee costs the same however often you trade, so it doesn't change the answer. |
| Years | How long you'll keep this up |

## How it works

For every strategy from "buy every period" to "buy every 52 periods", the workbook:

1. Lets each period's savings sit in the savings account, earning interest, until it's time to buy.
2. Invests the whole amount at once, less the brokerage fee.
3. Grows each purchase at the expected return until the end.
4. Adds up the investments plus any savings not yet invested at the end.

The strategy with the highest end value wins. The full working for every strategy is on the **Strategies** tab.

Each strategy's end value is calculated exactly, not estimated. If each purchase invests *E* dollars after the fee, there are *m* purchases every *k* periods over *N* periods, and *g* is the investment return per period, then the investments are worth *E × G* at the end, where

$$G = (1+g)^{N-mk}\cdot\frac{(1+g)^{mk}-1}{(1+g)^{k}-1}$$

*G* (the "growth multiplier") is what $1 put in at every purchase would be worth at the end. It's a geometric series: the first purchase grows for almost the whole period, the last for only a few periods.

The per-period return is converted from the yearly figure by compounding, *g* = (1 + yearly return)^(1/periods per year) − 1, so it adds up to exactly the yearly return over a year.

### Rule-of-thumb check

The Calculator also shows a quick approximation: buy whenever your savings reach

$$\sqrt{\frac{2 \times \text{fee} \times \text{yearly savings}}{\text{expected return} - \text{savings rate}}}$$

This has the same square-root form as Baumol's 1952 inventory model of how much cash to hold. For the example above it suggests about every 17 weeks, close to the exact answer of 18.

## Validation

The **Validation** tab checks the exact formula against a separate program that steps through every single period one at a time. They agree to the cent.

The **18 week buying cycle** tab is a worked example for the settings above: one row per purchase, showing how long each one is invested and what it grows to. Added to the savings left uninvested at the end, the rows sum to the Calculator's figure.

## What it doesn't do

- **Predict the market.** It uses one average expected return, so it tells you *how often* to buy, not *when* prices are low.
- **Account for risk.** Real returns go up and down. Holding a few weeks of savings in cash changes your risk very slightly, which barely matters over years.
- **Account for tax**, or changes to fees and interest rates over time.

If your broker charges nothing per trade, you don't need this: buy every period.

## Tabs

| Tab | Contents |
|---|---|
| Read Me | Instructions and explanation |
| Calculator | Inputs, the answer, the rule-of-thumb check and a chart |
| Strategies | Full working for every buying frequency |
| 18 week buying cycle | Purchase-by-purchase worked example |
| Validation | Checks against an independent simulation |

## Colour key

- **Blue text on light blue:** an input you can change
- **Black text:** calculated by a formula
- **Light green:** an independent reference value used for checking
- **Light amber:** a warning or caveat

## Reference

Baumol, W. J. (1952). The transactions demand for cash: an inventory theoretic approach. *Quarterly Journal of Economics*, 66(4), 545–556.

---

Built by Kieren Watkins as part of a portfolio of free tools.
