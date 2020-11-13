# Automatic-Rebalancing

The following project aims at decreasing manual workload and the cost of month-end fixed income portfolio rebalancing. At the end of each month, the benchmark for the fixed income portfolio changes, which, in turn, changes the net exposure of the portfolio. Hence, the need to rebalance the portfolio and return it to the original state. For the code to independently carry out the task, the rebalancing process has to be divided into several parts.

First, the key rate durations of a desirable trade need to be identified. In the case of pure rebalancing, duration of the trade equals the difference between exposures of the projected and current benchmarks. Second, it is essential to identify the pool of potential securities and to construct the rebalancing trade. Finally, after selecting the most attractive set of bonds, the code adjusts the size of each position to achieve a desirable net exposure. The code also minimizes the residual cash after the rebalancing, as well as the net size of the trade.

At all times, there are around 300 US treasuries available to purchase, each with different maturity, coupon, and duration. Hence, a bond price is not a useful indicator of its attractiveness. To differentiate between the treasuries, the code calibrates the Nelson Siegel Svenson model (1994) and fits the treasury yield curve. Each treasury is then re-priced using the new yield curve. The lower the actual price compared to the fitted prices of the treasury, the higher the probability that it will be purchased, and the lower the probability that it will be sold for the rebalancing. The logic works in reverse for treasuries that are more expensive than their fitted price.

Figure 1 shows the key rate dollar duration of the portfolio and the original benchmark. The difference between the two or the net exposure of the portfolio is shown in the second axes. Figure 2 shows the key rate dollar duration of the portfolio and the new benchmark. It can be seen that substituting the benchmark changes the net exposure of the portfolio. Figure 3 shows the difference between the two net exposures, which is the characteristic of the trade the code will try to construct.

After selecting the securities and the characteristics of target trade, Nelder–Mead minimization algorithm minimizes the root squared error consisting of weighted key rate duration and residual cash errors, as well as the size of the trade.

The user specifies the desired number of trades before the optimization. The table shows the resulting five trade rebalancing. This example presents the most straightforward use of the program, which can also be used to turn investment ideas into trades. While the program can measure the other instruments, as presented in Figure 4, it is not able to trade them. More work is required to allow the program to trade them.



NOTE: Running the application requires a working Bloomberg terminal
