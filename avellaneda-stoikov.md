# High-frequency trading in a limit order book by Avellaneda and Stoikov
https://math.nyu.edu/~avellane/HighFrequencyTrading.pdf

## Introduction
This paper comes up with two formulae for dealers (market makers) to use to determine how to quote bids and asks. The first equation is the reservation price equation, which determines a single price to quote above and below. This reservation price is essentially a personalized mid-price based on the fair value of the security and adjusted for the dealer’s inventory risk. The second formula is the bid-ask spread formula, which determines how far away from the aforementioned reservation price the dealer should quote.

In the authors' words:
> The main result is that the optimal bid and ask quotes are
derived in an intuitive two-step procedure. First, the dealer computes a personal indifference valuation for the stock, given his current inventory. Second, he calibrates his bid and ask quotes to the limit order book, by considering the probability with which his quotes will be executed as a function of their distance from the mid-price. In the balancing act between the dealer’s personal risk considerations and the market environment lies the essence of our solution.

## Equation Breakdown
### Eq 29, reservation price formula:
$$r(s,t)=s-q\gamma\sigma^2(T-t)$$
The reservation price can be broken down into two parts: $s$ and $q\gamma\sigma^2(T-t)$. $s$ is simply the current price of the asset. This is typically the mid-price of the asset. In this equation, $s$ is subtracted by what we will call the "adjustment factor." The adjustment factor is broken down into the following components:
- $q$, the dealer's inventory (i.e. position). Dealers view inventory as risk. Because they want to stay market-neutral, they want to keep a flat position as much as possible. If the dealer's inventory is positive (they are net long the asset), then the reservation price will be lower than the mid-price in an attempt to sell quicker. Conversely, if the dealer's inventory is negative (they are net short the asset), then the reservation price will be higher than the mid-price in an attempt to buy quicker. If the dealer's inventory is neutral ($q=0$), then they are indifferent and are fine with simply quoting symmetrically around the mid-price. Additionally, note that the adjustment factor is proportional to $q$; the more inventory is accumulated, the greater the adjustment should be to avoid taking on more risk.
- $\gamma$, the inventory risk parameter (i.e. the dealer's risk tolerance). This is a number typically $0\lt\gamma\le1$ where 1 is very risk averse. A higher inventory risk parameter will try to avoid accumulating an inventory. If the dealer is not very risk averse (low $\gamma$), then they will not bother to adjust their reservation price very much in response to accumulating inventory. This makes sense because the adjustment factor is proportional to $\gamma$.
- $\sigma^2$, the variance of the asset. This input tells us "how risky" the asset is, in terms of how much the price may move in a single timestep. As you can see in the equation, the adjustment factor is proportional to $\sigma^2$. We can think of variance as an amplifier of $q$, where $q$ is how many units of inventory (risk) we have, and $\sigma^2$ is a measure of how volatile a unit of inventory is. Intuitively, if we expect the price to move a lot within the very near future, we want to eliminate our exposure to this movement as soon as possible.
- $(T-t)$, the amount of time until the terminal time (typically market close). As we approach terminal time, the inventory position is considered less risky as there is less time for the price to move far away from the current price. If you are familiar with options pricing theory, this concept is similar to theta. The adjustment factor is proportional to $(T-t)$. As we approach terminal time, $(T-t)\to 0$, effectively "dampening" the adjustment factor.

In summary, the reservation price is just the mid-price subtracted by the amount of risk (relative to their risk tolerance) that the dealer currently owns.

### Eq 30, bid-ask spread formula:
$$\delta^a+\delta^b=\gamma\sigma^2(T-t)+\frac{2}{\gamma}\ln(1+\frac{\gamma}{\kappa})$$

The bid-ask spread can also be broken down into two parts: $\gamma\sigma^2(T-t)$, which we recognize from the reservation price equation, and $\frac{2}{\gamma}\ln(1+\frac{\gamma}{\kappa})$, an expression that introduces a new variable, $\kappa$. As you may recall from the prior explanation, $\gamma\sigma^2(T-t)$ is a measure of how risky a unit of inventory is given the dealer's risk tolerance. This piece makes sense because market makers want to widen their spread in response to volatility. Furthermore, the spread is also a decreasing function of time. At the end of the day, the market maker wants to be flat and not hold any risk overnight, so the spread must narrow in order to liquidate before market close.

The second piece in the equation, $\frac{2}{\gamma}\ln(1+\frac{\gamma}{\kappa})$, is less intuitive. Let's first understand $\kappa$, the arrival rate of orders.

## Building Up To The Equations
