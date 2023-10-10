# How Not To Be Wrong

## Info
- Type: book
- Author: TODO

## Category
Math, theoretical, using normal experience/examples

## Summary 
Common pitfalls when you lack math intuition, introduced via social/political
phenomenon/issue.Provide mathematical tools & principles to understand and deal with
some daily events/problems.

## Structure
- Intro: math as an aid for understanding
- I - Linearity:
  - Linear ns nonlinear
  - Curve as line. Calculus.
  - Linear regression
  - Thinking in proportion
  - Law of large numbers
  - Proportion in the present of negative number
- II - Inference:
  - Wiggle room aka cherry picking
  - Standard statistical test (null hypothesis significance test) & its problem
  - Dif between proof by contradiction and null hypothesis reasoning
  (not logically sound)
  - Problem of current scientific standard & practice using a fixed p-value = 0.05
  - Conditional probability & Bayesian inference
- III - Expectation:
  - Expected value
  - Economic utility
  - Reduce variance
  - Error correction when transmitting info
- IV - Regression:
  - Regression to the mean
  - Correlation
  - Scatter plot
  - Correlation != causation
  - Correlation from common effect
- V - Existence:
  - Issue of current voting systems
  - Effect of irrelevant alternatives
  - Formalism in math & politics
- How to be right: work with uncertainty, be skeptical.

## Author's problem & resolution
- Show that many daily problems are related to math: OK
- Provide math tools to extend common sense, avoid being wrong, understand the world
in a deeper way: OK

## Main arguments

### Intro
- Why math training in imp: improve intuition. Math in every aspect of life.  
-> math as an aid for understanding, avoid being wrong
- Lessons from Abraham story:
  - Check assumptions
  - Abstraction: solve problems in dif areas
  - Survivorship bias
- Math is/derived from common sense. Useful math must include abstract reasoning
& intuition
- 4 types of math:
- |          | Simple                 | Complicated        |
  |----------|------------------------|--------------------|
  | Profound | In the book            | For mathematicians |
  | Shallow  | 1+2=3 sin2x=2sinx.cosx | School math        |
- School math problem:
  - Treat math as set of unquestionable facts & rules
  - Doesn't enrich knowledge about the world
- Math in this book: principles, tools to avoid being wrong

### I - Linearity

#### 1. Linear vs nonlinear
- Linear reasoning: more is good/bad
- Nonlinear curve: peak in the middle  
-> Which way to go depends on where you are
- Fallacy: It could be the case -> I want it to be the case -> It is the case

#### 2. Curve as line. Calculus.
Small part of a curve can be represented as line

#### 3. Linear regression
- Simple but not work in nonlinear cases  
-> Need to decide whether to use
- Discussion about math teaching: should combine traditional algo & precision with
discovery & approximation

#### 4. Thinking in proportion. Law of large numbers
- Math hygiene: test a math method by computing the same thing in several dif ways
- Assessing cases where number is small: if there is adverse result, can assume it is
due to luck  
-> Will regress to the mean
- Illusion of averages: 5 heads -> next flip likely to be tail  
-> Can doubt the fairness of the coin  
-> Law of large numbers: dilute what already happened with new data (first 5 heads
become less imp when more flips are made)
- Compare in terms of proportion: only meaningful in limited cases
(eg proportion is big)

#### 5. Proportion in the present of negative numbers
- Meaningless, as part/sum of parts can > 100% of sum  
eg: A gain 500, B lose 400 -> A 500% total
- Math vs computation: math = figuring out which computations to perform
to derive meaning

### II - Inference

#### 6. Wiggle room aka cherry picking
- Baltimore stockbroker: swayed by impressive results, don't know how many chances
he got to get those results  
-> Improbable things happen a lot
- Wiggle room make it hard to draw reliable inferences from improbable events

#### 7. Standard statistical test (null hypothesis significance test) & its problem
- Reverse engineering (build theories from observations) is hard: many
competing/possible theories
- Frequentist view of probability: p(X) = a% -> given large number of situations with
similar condition, X will happen a% of the time
- Language when talking about chance is ambiguous: use probability to talk about
events that happen only once (not subject to chance)
- Probable or improbable depends on the set of hypotheses we made about the underlying
mechanism of the world
- Many scientific questions are yes/no questions: does it have effect/cause sth?  
-> Null hypothesis: it has no effect
- Procedure of null hypothesis significance test:
  1. Run an experiment
  2. Calculate the probability (p) of getting the result as observed if the null hypo
  is true
  3. If p < a threshold (p-value, usually chosen as 0.05) -> the result is
  statistically significant
- -> Popular because it is similar to our intuitive reasoning about uncertainty
- -> Standard method for assessing the results of scientific research
- Problems:
  - "Significant" here != important/meaningful: only means the effect is not zero  
  -> Effect could be so small that shouldn't be attended to  
  -> Issue of using risk ratio: eg: 7 times of 1/1M
  - Null hypo almost always false: doing sth will always have some effect
- Low vs high-powered study:
  - Low: might not be able to detect an effect
  - High: might detect an unimp, small effect
- Human:
  - Quick to perceive patterns when they don't exist
  - Overestimate the strength of the pattern if it exists

#### 8. Dif between proof by contradiction and null hypothesis reasoning (not logically sound)
| Proof by contradiction       | Null hypothesis reasoning       |
|------------------------------|---------------------------------|
| Suppose hypothesis H is true | Suppose null hypo H is true     |
| -> Fact F can't be the case  | -> Outcome O is very improbable |
| But F is the case            | But O was actually observed     |
| -> H is false                | -> H is very improbable         |
- Problem: improbable is not impossible

#### 9. Problem of current scientific standard & practice using a fixed p-value = 0.05
- p-value = 0.05 -> if H is true, there is 5% chance that the exp returns a statistical significant result  
-> 5% of exp are publishable
- Exps that failed to replicate the original exp won't be published coz no statistical significant result is found
- When number of things with real effect is small & the study is low-powered:
overwhelmed by things with no effect but pass the test
- Treat a continuous variable as a binary one  
-> Scientists might try to cheat the data to make it past p-value  
-> Insignificant data should be reported
- How to make better inference:
  - Decide p-value flexibly
  - Replication. A statistically significant result is only a beginning, a suggestion
  for research in that direction
  - Report confident interval in addition to probability under H  
  -> Consider not only H but a whole range of alternatives
- Confident interval (CI): range of hypotheses with p > p-value  
eg: that the effect is from 3% to 17% all > p-value -> CI = 3-17%
  - If CI include 0 -> H is not excluded:
    - CI range is small (-1 - 1%): no effect
    - CI range is big (-20 - 20%): don't know the direction of the effect or if there
    is an effect
  - If CI not include 0 -> effect small or large depend on the interval. CI range
  is big -> not sure
- -> CI inform how to act, not what to believe (eg true/false)

#### 10. Conditional probability & Bayesian inference
- Problems with algo & machine learning: can't handle chaotic systems (eg weather)
- Human behaviors: might be harder than weather, since no good math model (yet?)
- Why big companies try to improve their models: small improvement in accuracy could
lead to high increase in profit & competitiveness
- Conditional probability: the prob that X is the case, given that Y is:  
P(X|Y) = P(X^Y)/P(Y) != P(Y|X)
- People tend to make choice deviate from randomness when they try to resemble
randomness: BRBBR > BBBRR
- Bayesian inference (often used in ML):
  - Assign each theory a prior prob
  - Compute posterior prob of each theory in light of evidence  
  -> View prob as degree of rational belief in a hypo in light of given evidence  
  -> Null hypo significance test is non-Bayesian
- People usually assign prior prob:
  - Simple theories > complicated theories
  - Theories based on things they already know > theories suggesting novel phenomena
- Conspiracy theories: designed to avoid being touched by new evidences
- Need to consider dif competing theories (& unknown ones) when trying to
make inference
- Some problems are non-quantitative, shouldn't be assigned a prob

### III - Expectation

#### 11. Expected value
- Expected value: average value when taking many same bets
- Value of life insurance = expected years left x year value

#### 12. Economic utility
- Utility:
  - Tool for deciding what to do: rational agent make decision to
  maximize utility
  - Depends on personal evaluation -> should be careful when making generalization
- In practice, very low prob can be 0 if you rarely take the chance
- Risk vs uncertainty
  - People prefer choices with fixed chance (risk)
  - Uncertainty: probability can't be measured  
  -> Can't be handled by math analysis
- Role of math in science:
  - Construct formalisms (generalizations)
  - Understand the limit of those formalisms

#### 13. Reduce variance. Error correction when transmitting info.
- More capital -> can take more risk (no chance of defaulting)
- Variance: how widely spread out the possible outcomes of a decision are &
how likely to encounter extremes on either end  
-> People want to build:
  - Low-variance portfolios (positive expected value)
  - Big-variance for negative expected value
- Error correcting code: communication protocol that allow receiver to correct noise
in a signal  
-> To avoid having to repeat a bit many times, use codes with high distance
- Why people by lottery:
  - For fun
  - Prospect theory & insensitivity to small probability

### IV - Regression

#### 14. Regression to the mean
- Usually occurs in situations that involve random fluctuations in time (variable
affected by both stable factors & chance): extreme results due to luck regress
towards medium results  
-> Resistant to cause-seeking human
- Situations where regression to the means is due to other forces, not chance:
mediocre stay mediocre, not become extreme

#### 15. Correlation. Scatter plot.
- Scatter plot: can be used to explore relationship of 2 variables (easy for human to
interpret, compared to table of data)
- Isoplepth: curves where density of points was roughly constant  
-> High correlation (var 1 determine var 2): ellipse with high eccentricity (skinnier)
- Good prediction model: remove highly correlated vars
- Algebra adv: easy to formalize & type into computer
- Geometry adv: close to human physical intuition
- Correlation as vector: length in each dimension is the value of an instance in
the sample:
  - Highly correlated -> angle between 2 vectors is small
  - Not correlated: angle = 90
  - Negatively correlated: angle > 90
- Correlation is not transitive: A correlated with B (eg 60 degree), B with C (60 deg),
but A might not cor with C (60 + 60 = 120 degree)  
-> Can't chain effects together (eg medicine)
- Uncorrelated (no linear relationship) != unrelated (no relationship)

#### 16. Correlation != causation. Correlation from common effect.
- Decide causation from correlation is hard  
-> Might still need to act (eg policy) when the casual link is not clear
- Correlation from common effect: when the sample is not a random sample of
the population -> positive/negative correlation. Example: in hospital:
  - 20 with disease A, not B
  - 20 with disease B, not A
  - 60 with A & B  
- -> 60% have both A & B, 3x only A/B. Not because A correlated with B, but because
  having both A & B make it likely to be in hospital

### V - Existence

#### 17. Issue of current voting systems. Effect of irrelevant alternatives.
- Problem of aggregating opinions: eg: dealing with budget deficit:
  - 1/3 want raise taxes, keep A & B benefit
  - 1/3 want cut spending on A
  - 1/3 want cut spending on B
- -> 2/3 don't want to raise tax, 2/3 want to keep A, 2/3 want to keep B  
-> Can be framed in dif ways
-> "Majority rules" system only work when there are 2 options
- Effect of irrelevant alternatives: eg:
  - A > B > C: 40%
  - B > A > C: 30%
  - C > B > A: 30%
- -> A win, but 60% choose B > A
- How to manipulate choices: introduce a mostly same but slightly worse alternative: eg:
  - A > B > C: 50%
  - B = C > A: 50%
- -> B: 75%, A: 50%

#### 18. Formalism in math & politics
- Correctness (what is true) vs formalism (what follows the rules)

### How to be right: Work with uncertainty. Skepticism.
- Math as a quantitative tool to reason about uncertainty  
-> Make decision & take action
- Try to disprove your belief  
-> Know more about why you believe it

## Criticism
- Chapter naming is very obscure, hard to get what the chapter is about by reading it
- Style: lots irrelevant discussion/digression. Examples sometimes too long for 
a small point: eg: Part 1: Chap 1-3, 5, is of considerable size but not many points
- Many ideas not entirely new, mentions in other books (eg Thinking, fast and slow):
  - Non-linearity
  - Law of large numbers
  - Cherry-picking
  - Expected value
  - Economic utility
  - Regression to the mean
  - Correlation != causation
  - Difficulty of extracting public opinion

## Takeaways
- Standard statistical test (null hypothesis significant test)
- Problems of current scientific standard & practice using fixed p-value=0.05
- Bayesian inference