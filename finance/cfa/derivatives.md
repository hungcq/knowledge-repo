# Derivatives
- Hedge ratio in one-period binomial model for option valuation:
  - hSt(up) - ct = hSt(down) -> h -> hS0(up) - c0 = (hSt(up) - ct) / (1 + r) -> c0
- Risk neutrality model: option value = (value up x P(up) + value down x P(down)) / (1 + r)

## Concept review
- Convenience yield
- American call option is valuable when?
- Swap as a series of FRAs
- Cash-settled contract (vs deliverable contract)
- Hard commodities vs soft commodities
- OTC derivatives (vs exchange traded)
- Credit default swap
- Option premium
- Hedge accounting
- Net cost of carry
- Par swap rate
- Swap price
- Cost/benefit of holding asset's effect on call/put option value
- Hedge ratio
- Params of risk neutrality model

## Concept answer
- Convenience yield = non-monetary benefits of holding an asset
- American call option is valuable if exercise early can provide cash flow (eg bond's coupon)
- Swap as a series of FRAs:
  - Each FRA has rate = swap fixed rate
  - Value of each FRA != 0. First value is known at initiation (using MRR at initiation & F)
  - Sum of values of all FRA = 0 at initiation
  - Valuation: MRR1 / (1 + S1) + MRR2 / (1 + S2) ^ 2 + ... = F / (1 + S1) + F / (1 + S2) ^ 2 + ...
  - -> Calculate expected forward rates (MRRs) using spot rate (S), then solve for F
- Cash-settled contract (vs deliverable contract): only gains/losses are exchanged at settlement
- Hard commodities (eg mine, gold, oil) vs soft commodities (eg cotton, coffee, pork, cattle)
- OTC derivatives (vs exchange traded): customizable, less regulated & less transparent
- Credit default swap: protection buyer makes fixed payments on settlement dates,
protection seller pays only if the underlying (eg reference security) has a credit event (eg bond default, corp bankruptcy)
- -> ~ insurance
- Option premium: price, = time value + intrinsic value
- Hedge accounting: derivative hedge reduce volatility of asset price on balance sheet. Types:
  - Cash flow
  - Fair value
  - Net investment: value of equity of a foreign subsidiary
- Net cost of carry = benefit - cost
- Par swap rate: fixed rate at which sum of PV of FRAs of swap is 0
- Swap price: fixed rate
- Cost/benefit of holding asset's effect on call/put option value: higher cost, higher call value
- Hedge ratio: number of shares of the underlying for each call option written, so that up move value = down move value
- Params of risk neutrality model:
  - Asset price at t0
  - Asset price of up/down move (volatility)
  - Risk-free rate
  - Option exercise price
- -> Risk neutral prob calculated from size of move & risk-free rate