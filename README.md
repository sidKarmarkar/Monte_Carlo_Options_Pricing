## Overview

This project implements a Monte Carlo simulation to price European call options using Python. The Monte Carlo method is widely used in quantitative finance to simulate the underlying asset prices over time and calculate the option's price based on these simulated outcomes.

The simulation uses **Geometric Brownian Motion (GBM)** to model stock price movements, which is a mathematical representation of the random behavior of financial markets. By running a large number of simulations, we can estimate the expected payoff of the option and use that to determine the option's fair price.

This project is part of my personal learning journey in quantitative finance and computational methods, aiming to integrate AI/ML techniques with traditional quantitative methods. It also helps me explore the potential of Python in the world of financial modeling.

---

## Project Structure

- `monte_carlo_options_pricing.py`: Main script that contains the implementation of the Monte Carlo simulation for pricing options.
- `README.md`: Documentation for the project, including setup instructions and an explanation of the code.
  
---

## Key Concepts

- **European Call Option**: A type of option that gives the holder the right, but not the obligation, to buy an asset at a specified price (strike price) on a specific date (maturity).
- **Monte Carlo Simulation**: A computational technique that uses random sampling to estimate mathematical quantities. In this project, it simulates possible stock price paths and calculates the average payoff to estimate the option price.
- **Geometric Brownian Motion (GBM)**: A stochastic process used to model stock price movements over time, assuming that returns are normally distributed and that stock prices follow a continuous path.
  
---

## Requirements

This project uses Python and a few standard libraries. To install the necessary libraries, you can use `pip`:

```bash
pip install numpy matplotlib
```

---

## Parameters and Usage

In this implementation, the following parameters are used:

- `S0`: Initial stock price (e.g., $100).
- `K`: Strike price (e.g., $110).
- `T`: Time to maturity (e.g., 1 year).
- `r`: Risk-free interest rate (e.g., 0.05 for 5%).
- `sigma`: Volatility of the stock (e.g., 0.2 for 20%).
- `n_simulations`: Number of Monte Carlo simulations (e.g., 10,000).
- `n_steps`: Number of time steps in the simulation (e.g., 252 steps for daily intervals over one year).

### Running the Code

To run the Monte Carlo simulation for pricing a European call option, simply execute the `monte_carlo_options_pricing.py` script:

```bash
python monte_carlo_options_pricing.py
```

The script will simulate stock price paths and estimate the option price based on the average discounted payoff from all the simulations.

### Example Output

```bash
The estimated price of the European Call Option is: $5.82
```

The result may vary slightly each time due to the random nature of the simulation.

---

## Code Breakdown

### Simulating Stock Prices

The function `simulate_stock_price()` uses **Geometric Brownian Motion** to simulate multiple stock price paths over time. It takes the initial stock price (`S0`), the time to maturity (`T`), the risk-free rate (`r`), and the volatility (`sigma`) as inputs, and generates a matrix of stock prices for a given number of simulations and time steps.

```python
def simulate_stock_price(S0, T, r, sigma, n_simulations, n_steps):
    dt = T / n_steps  # time step
    stock_paths = np.zeros((n_simulations, n_steps + 1))
    stock_paths[:, 0] = S0
    ...
    return stock_paths
```

### Monte Carlo Simulation for Option Pricing

The main function, `monte_carlo_option_pricing()`, calls the stock price simulation function and calculates the payoff of the option (the difference between the final stock price and the strike price for a call option). It then averages these payoffs across all simulations and discounts them back to the present value to estimate the option price.

```python
def monte_carlo_option_pricing(S0, K, T, r, sigma, n_simulations, n_steps):
    stock_paths = simulate_stock_price(S0, T, r, sigma, n_simulations, n_steps)
    payoff = np.maximum(stock_paths[:, -1] - K, 0)  # Call option payoff
    option_price = np.exp(-r * T) * np.mean(payoff)  # Discounted payoff
    return option_price
```

### Visualization

To help visualize the random nature of stock price movements, the script plots several simulated stock price paths:

```python
plt.plot(stock_paths.T, lw=1)
plt.title('Simulated Stock Price Paths')
plt.xlabel('Time Steps')
plt.ylabel('Stock Price')
plt.show()
```

This gives you a better understanding of how the price evolves over time for each simulation.

---

## Why Monte Carlo for Option Pricing?

Monte Carlo simulations are particularly useful for pricing complex derivatives like path-dependent options or options with multiple sources of uncertainty. Although simpler methods such as the Black-Scholes formula exist for European options, the Monte Carlo approach provides a flexible framework that can be easily extended to more complex financial products.

---

## Conclusion

This project provides a basic yet powerful framework for pricing European call options using Monte Carlo simulations. By experimenting with different parameters and methods, it offers a solid introduction to quantitative finance and the practical applications of Python in financial modeling.

Feel free to fork the repo, play around with the code, and reach out if you have any questions or ideas for improvements!

---

### License

This project is open-source under the MIT License, so feel free to use it for educational purposes or to build upon it.

---

Let me know if you'd like any additional information or changes for your README!
