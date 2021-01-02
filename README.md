# Single-Timeseries-Crypto-Bot
In this collaborative project we build a trading bot, which analysis a single timeseries of crypto currency prices to identify optimal conditions for entry and exit trades in real-time.

# Testing a QLearning Strategy by Monthe Carlo Simulation

For multiplereasons, a single simulation of a Q-Learning model is not yielding a realistic idea of the expected return generated by this strategy. Some notable arguments for the neccessity of running multiple simulations are the following.

- The decision rule of the Agent (Q-Tabel) is initialized by random values, a strategy/q-table that might perform well in sample can still have no predictive power. When such a table is tested outsied the sample data it might reveal that any in sample returns were purely based on a spureous correllation.
- The simulator class utilizes random numbers to simulate market prices. However, a single simulation might result in a performance that is rather driven by lucky random prices than by a feasable trading strategy. Outperformance is less likely over longer simulation periods, but there is always a small probability that a single simulation performs well because of such random prices and not because of the quality of the strategy itself.
- A single simulation might get stuck with suboptimal bahavior and thus not find an optimal solution.(Eventhough this is unlikely due to the Q-Learning algo including random exploration)

For each of the above reasons it is desirable to run multiple simulations and consider their distribution rather than a single realization of these strategies. This would also be optimal for the afore discussed "Simple Strategies". However, these follow a purely deterministic decision rule, while the q learning is even more vulnerable to random effects, due to the random initialization of the model.
The below plot shows a Q-Learning algorithm (features: 1 period return, 60 periods return, 20 periods deviation from mean, 60 period deviation from mean, 14 periods RSI, Actions: 0% BTC, 50% BTC, 100% BTC in the Portfolio) using simulated market orders. The black line indicates the average performance for Dec 2019 over 100 simulations with different random seeds. While the blue areas mark the 100%, 90%, 60% probability mass of returns generated by such a strategy. Notably, the red line displays the performance of a 100% exposure to BTC for the same period. While at first sight the strategy appears to outperfrom a simple long exposure to Bitcoin it mus be noted that the simulation did not account for any transaction costs like comissions, or spreads and fruthermore, it does not take into account liquidity constraints. Therefore, while the strategy might be capable of identifying those moment in wich holding BTC is relatively desirable, it cannot be expected that deploying such an algorithm does result in outperforming BTC and might not even generate positive returns at all.
![](https://github.com/Tobias-Mann/Single-Timeseries-Crypto-Bot/blob/main/Images/MonteCarloDistribution.png?raw=true)
