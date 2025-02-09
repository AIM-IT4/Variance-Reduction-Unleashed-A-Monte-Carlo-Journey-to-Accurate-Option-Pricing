# Variance Reduction Unleashed: A Monte Carlo Journey to Accurate Option Pricing

## Introduction

This project demonstrates how to price a European call option using Monte Carlo simulation techniques. Three different Monte Carlo methods are implemented:

1. **Simple Monte Carlo**
2. **Antithetic Variates**
3. **Control Variates**

In addition to pricing, the project includes:
- **Convergence Analysis:** Visualizing the cumulative average of discounted payoffs using 1,000 simulation paths for each method.
- **Stock Price Path Simulation:** Simulating full asset paths over one year (252 trading days) to observe the evolution of the underlying stock.

## Theoretical Background

### Black-Scholes Model

The theoretical price of a European call option is given by the Black-Scholes formula:

$$
C = S_0 \, N(d_1) - K \, e^{-rT} \, N(d_2)
$$

where

$$
d_1 = \frac{\ln(S_0/K) + \left(r + \frac{1}{2}\sigma^2\right)T}{\sigma\sqrt{T}}, \quad
d_2 = d_1 - \sigma\sqrt{T}
$$

- $S_0$: Initial stock price  
- $K$: Strike price  
- $T$: Time to maturity (years)  
- $r$: Risk-free interest rate  
- $\sigma$: Volatility  
- $N(\cdot)$: Cumulative distribution function (CDF) of the standard normal distribution

### Monte Carlo Simulation for Option Pricing

The underlying asset price is modeled using geometric Brownian motion:

$$
S_T = S_0 \exp\left[\left(r - \frac{1}{2}\sigma^2\right)T + \sigma\sqrt{T} \, Z\right]
$$

with $Z \sim N(0,1)$. The discounted payoff of a European call option is:

$$
\text{Payoff} = e^{-rT} \max(S_T - K, 0)
$$

The Monte Carlo estimator for the option price is the average of these discounted payoffs across many simulated paths.

### Variance Reduction Techniques

Monte Carlo simulation can suffer from high variance, making convergence slow. Two common variance reduction techniques are used:

1. **Antithetic Variates:**  
   For each random sample $Z$, its negative $-Z$ is also used. This produces paired estimates that tend to cancel out some of the random noise:
   
   $$
   \text{Payoff}_{\text{antithetic}} = \frac{1}{2}\left[\max\left(S_T(Z) - K, 0\right) + \max\left(S_T(-Z) - K, 0\right)\right]
   $$

2. **Control Variates:**  
   A control variate with a known expected value is used to adjust the payoff. In this project, the terminal stock price $S_T$, which has an expected value of $S_0 e^{rT}$, is used. The adjusted payoff is:
   
   $$
   \text{Payoff}_{\text{adjusted}} = \text{Payoff} - c \left(S_T - S_0 e^{rT}\right)
   $$
   
   where $c$ is an optimal coefficient computed based on the covariance between the payoff and $S_T$.

### Stock Price Path Simulation

To simulate full asset paths over a one-year period (with 252 trading days), the following discrete-time approximation of geometric Brownian motion is used:

$$
S_{t+\Delta t} = S_t \exp\left[\left(r - \frac{1}{2}\sigma^2\right)\Delta t + \sigma\sqrt{\Delta t} \, Z\right]
$$

with $\Delta t = \frac{T}{252}$ and $Z \sim N(0,1)$.

## Project Structure

- **Price Calculation:**  
  The Black-Scholes formula is used for the theoretical price, while the three Monte Carlo methods (Simple, Antithetic, and Control Variate) are implemented with 100,000 simulation paths for high accuracy.

- **Convergence Analysis:**  
  For each Monte Carlo method, the cumulative average of the discounted payoffs is computed using 1,000 simulation paths. These convergence plots help visualize how quickly the estimator stabilizes.

- **Stock Price Simulation:**  
  Full stock price paths are simulated over one year (252 trading days) for each Monte Carlo method. This provides insight into the dynamics of the underlying asset.

## Conclusion

This project illustrates the practical implementation of Monte Carlo simulation methods for option pricing, highlighting the use of variance reduction techniques to improve efficiency. The convergence plots and stock price path simulations offer valuable visual insights into both the estimation process and the behavior of the underlying asset over time.

*Prepared by: Amit Kumar Jha* 

*Date: 2025-02-09*
