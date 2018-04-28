---
title: "Application of Utility Theory to A Simple Bet"
author: "Brian Montgomery"
date: "April 28, 2018"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

Utility theory places a value on having a certain wealth. It provides a consistent framework for evaluating all kinds of contingent financial transactions from insurance to gambling.

A utility function u(w) is a simple expression of the utility $(u)$ of wealth $(w)$. Utility functions typically have negative second derivatives, as this it the feature that makes buying insurance attractive. And gambling without an advantage unattractive.

A certain class of utility functions, called "Constant Relative Risk Aversion" (CRRA) are especially useful.  They express a consistent level of risk-reward trade-off.

The Arrow-Pratt measure of risk aversion (RRA) is defined as: $RRA = \frac{-w u''(w)}{u'(w)}$

For a given individual situation this will typically be constant over a wide range of wealth sizes. So the CRRA criterion becomes a differential equation for $u(w)$: $$w u'' + RRA u' = 0$$

The solutions to which are $u \propto log(w)$ for RRA = 1, and $u \propto -w ^ {(1 - RRA)}$ otherwise.

Logarithmic utility (RRA = 1) leads to the famous Kelly criterion of maximizing growth rate over time. But typically people are more risk averse than this (RRA > 1). And will value a lower volatility of returns as well as long-term growth.

Utility functions are the same under linear transformation, because only changes in value matter and because the same wealth can be measured in different units.

To illustrate how a utility function works, I'll apply it to a simple wager.  Start with wealth = $w_o$ and place a bet $b$ with probability $p$ of winning and decimal odds $d$.  This means a winning bet will pay $bd$ including return of the amount wagered.

Expected utility after the bet is then: $$E(u) = pu(w_ou + b(d - 1)) + (1 - p)u(w_o - b)$$
Maximizing this expected utility will tell us how much we should bet.
$$\frac{dE(u)}{db} = 0 = (d - 1)pu'(w_o + b(d - 1)) - (1 - p)u'(w_o - b)$$
To solve this in the case of a general utility function, we assume $b$ is small compared to $w_o$ and expand the utility near $w_o$ using a Taylor series: $$u'(w_o + \delta) \approx u'(w_o) + \delta u''(w_o)$$
With this approximation, we can solve the equation for b: $$b = \frac{-u'(w_o)(p(d - 1) - (1 - p))}{u''(w_o)(p(d - 1)^2 + (1 - p))}$$

Define $e = p(d - 1) - (1-p)$ as the edge or advantage on the bet. The bet should not be made at all unless this is positive.  The expected gain on the bet is just $be$.  Also substitute our earlier definition of RRA. So
$$b = \frac{ew_o}{RRA(p(d - 1)^2 + (1 - p))}$$
This expression shows most of the characteristics we would expect.  The bet should be in proportion to the original wealth $w_o$ and the edge $e$.  Also it should be inversely proportional to the relative risk aversion.

The remaining part of the expression, $p(d - 1)^2 + (1 - p)$ can be re-written in terms of the edge as $(d - 1) + e(d - 2)$.  For an even-money bet $(d = 2)$ the expression would just be 1.  For a relatively small edge, the expression becomes $d - 1$, the fractional odds.  The bet should be made in inverse proportion to the fractional odds. Or, in other words, two bets with the same small edge should be made to have the same potential net winnings. $$b \approx \frac{ew_o}{RRA(d - 1)}$$

This is the standard Kelly criterion bet with the RRA factor representing "fractional Kelly" betting.  Note that the relative attractiveness of any particular bet does not change with the relative risk aversion.  More risk-averse bettors can just bet a smaller fraction of their bankroll and still be near-optimal according to their own utility function.

The simplifying assumptions made were ignoring the higher-order terms in the Taylor series for $u$ (local parabola) and ignoring the relatively small term $e(d - 2)$ in the denominator.
