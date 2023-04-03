# High-frequency trading in a limit order book by Avellaneda and Stoikov
https://math.nyu.edu/~avellane/HighFrequencyTrading.pdf

## Introduction
This paper comes up with two formulae for dealers (market makers) to use to determine how to quote bids and asks. The first formula is the mid-price formula, which determines a single price to quote above and below. This mid-price is based on the fair value of the security and adjusted for the dealer’s inventory risk. The second formula is the bid-ask spread formula, which determines how far away from the aforementioned mid-price the dealer should quote.

## Mid-Price Formula
Eq 29: $$r(s,t)=s-q\gamma\sigma^2(T-t)$$

## Bid-Ask Spread Formula
Eq 30: $$\delta^a+\delta^b=\gamma\sigma^2(T-t)+\frac{2}{\gamma}\ln(1+\frac{\gamma}{\kappa})$$
