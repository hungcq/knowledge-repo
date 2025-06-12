# Clear-sighted Statistics

## Info
- Type: ebook
- Author: Edward Volchok
- URL: https://cuny.manifoldapp.org/projects/clear-sighted-statistics

## Category
- Math
- Statistics
- Probability
- Research methodology

## Structure


## Goals
<img src="./resources/clear-sighted-statistics-goal.drawio.svg"/>

## Terms
- Statistics: data derived from samples
- Parameters: data taken from the entire population
- Population: total people/things under investigation
- Data (plural of datum)
- Sampling error: stats value != param value
- Facts (empirical evidence): separated observations/measurements
- -> Vs value
- Latin letter (eg s): var of a sample
- Greek letter (eg sigma): data of a population
- Census: counting every element in a population
- Sampling frame: list of all elements in the population
- Measurement: assignment of numbers to variables
- Construct: abstract concept
- Instruments = questionnaires?
- Peer-reviewed journal: use a small panel of peers to validate/filter researches & recommend which to publish
- Probability:
  - Experiment: a planned process carried out under controlled conditions that lead to only 1 of several possible outcomes
  - -> Can be indefinitely repeated
  - Event: a set of outcomes when an experiment is conducted
  - Sample space: list of every possible events of an experiment
  - Outcome: the result of a particular experiment
  - ME, CE events
  - Independent events vs conditional/dependent events
  - Law of large number: as sample size increases, sample stats approach population params
  - -> Empirical probability approaches theoretical probability
  - Gambler fallacy (independent events)
  - Joint probability
  - Counting rules: multiplication, factorial, combination, permutation
  - Decision theory: method of decision-making by assigning probabilities to outcomes of a decision, then weight cost & benefit
- Probability distributions:
  - Random vars
  - Categorical vars vs quantitative vars (discrete, continuous)
  - Probability distribution: provide mathematical relationship of probabilities
  of different possible outcomes of an experiment/observation/trial
  - -> Can be expressed as math formula/table/chart
  - Expected value = weighted mean
  - Variance = sum((x-mean)^2.P(x))
  - Replacement/no replacement sampling techniques
- Confidence interval:
  - Def: a range of sample values likely to contain the population params
  - Point estimate: sample stats upon which the confidence interval is based
  - Confidence level: % certain that the confidence interval contains the params (usually 95%)
  - -> = 1 - significance level
  - Margin of errors (MoE): confidence interval = point estimate +- MoE
- Statistical power: the ability of the selected hypo test to uncover imp finding,
given the variability of the data & the size of the sample
- Hypothesis: a preliminary proposition that provides an explanation of some phenomenon, which can be tested
- -> In stats: a tentative stm about a population developed from a sample
- Theory: system of propositions that provide a unified explanation of phenomena
that have withstood repeated attempts to refute them
- -> Falsification might lead to paradigm shift:
open new approaches to understand phenomena that previously haven't been considered
- NHST:
  - Null hypo (H0): a proposition tested through falsification process
  - -> In stats: sample stats = population params, dif = sampling error
  - Alternative hypo (HA/H1): MECE with H0
  - p-value: the probability under a specific statistical model that the statistical summary of the data
  would be equal to or more extreme than its observed value

## Style
- Author's claim (ok):
  - Lots of data visualization
  - Tool: Excel (popular)
  - -> Complimented by G-power: null hypothesis testing
  - Multiple examples
- Good sense of humour
- Many interesting stories & useful definitions

## Takeaway
- Basic understanding of the research method used in social science/business
- Limitation of NHST and development in statistics field
- How to do stats on Excel
- Deeper understanding of NHST concepts & process, and usage of different types of tests
- Development in the field

## Summary
<img src="resources/clear-sighted-statistics.drawio.svg"/>

### Excel formulas
- MAX
- MIN
- POWER
- COUNTIF
- MODE.MULT: return an array of modes
- AVERAGE
- MEDIAN
- SKEW
- KURT
- GEOMEAN
- TRIMMEAN
- AVEDEV: calculate MAD
- VAR.P, VAR.S: variance
- STDEV.P, STDEV.S: std
- PERCENTILE.INC: percentile
- FACT: factorial
- COMBIN: combination
- PERMUT: permutation
- BINOM.DIST: binomial distribution
- HYPGEOM.DIST: hypergeometric distribution
- POISSON.DIST: Poisson distribution
- NORM.S.DIST: standard normal distribution -> probability from z-value
- NORM.DIST: normal distribution -> proba from x, mean, std
- NORM(.S).INV: z/x from proba
- F.INV, F.DIST: F distribution
- CONFIDENCE.NORM, CONFIDENCE.T: confidence interval for population mean with known/unknown population std
- TINV: t-value from probability
- CHISQ: Chi-square dist
- Correlation & regression:
  - CORREL: calculate r
  - RSQ: r^2
  - LINEST: least square line (combine SLOPE, INTERCEPT)
  - TREND: calculate predicted y
  - STEYX: standard error of estimate