# Intraday Trading with Linear and Logistic Regression

## Overview

This project implements supervised machine learning strategies for intraday stock trading. The objective is to predict same-day stock performance using only information that is available at the market open, ensuring that the model does not use any future information that would introduce look-ahead bias. Two predictive approaches are explored. The first strategy uses linear regression to estimate the closing price of each stock and selects the stock with the highest predicted intraday return for investment. The second strategy uses logistic regression to estimate the probability that a stock’s closing price will exceed its opening price and allocates capital based on these probabilities while incorporating risk control mechanisms.

## Dataset

The dataset consists of historical trading data for ten NASDAQ stocks: AAPL, ADBE, AMD, AMZN, AVGO, FB, GOOGL, MSFT, QCOM, and TWTR. For each trading day, the available information includes the opening price, closing price, and trading volume. To ensure a fair and realistic modeling setup, all predictors are constructed using only information that would have been available before the market opens on the trading day being predicted.

## Feature Engineering

To capture short-term market behavior, a set of lagged technical indicators is constructed for each stock. These features include past intraday returns, volume-related signals, overnight price gaps, volatility measures, and moving-average-based trend indicators. The lagged returns capture recent momentum and short-term dynamics, while volume-based features measure unusual trading activity relative to recent history. Gap features describe overnight movements between previous closing prices and current opening prices. Volatility indicators estimate recent variability in intraday returns, and moving-average signals help capture broader short-term trends. In total, twenty-three predictive features are generated for each stock.

## Trading Strategies

The first strategy uses linear regression models trained separately for each stock to predict the same-day closing price based on the engineered features. The predicted closing price is converted into a predicted intraday return using the observed opening price. Each day, the strategy selects the stock with the highest predicted return and invests the entire portfolio in that single stock, resulting in a fully concentrated allocation. The second strategy uses logistic regression to estimate the probability that the closing price will be higher than the opening price. These probabilities are transformed into portfolio weights by applying a probability threshold, selecting the strongest candidates, and scaling allocations based on recent volatility in order to control risk. This approach results in a probability-driven allocation strategy that balances expected return with risk considerations.

## Backtesting

The evaluation of both strategies is conducted through historical backtesting using a chronological data split. The training period covers January to May 2018, while June 2018 is used as a validation period for tuning hyperparameters. The final evaluation is performed on the test period from July to December 2018. The backtesting process begins with an initial capital of €10,000. Portfolio returns are calculated daily based on the chosen allocation and the realized intraday returns of the selected stocks. In addition to a continuous-weight simulation, an integer-share simulation is also implemented to ensure that the strategy behaves realistically when trading whole shares.

## Results

The experimental results show that the logistic regression strategy significantly outperforms the linear regression strategy during the test period. The linear regression approach grows the initial capital from €10,000 to approximately €10,666, corresponding to a return of about 6.7%. In contrast, the logistic regression strategy increases the capital to approximately €15,387, achieving a return of about 53.9%. The improved performance can be attributed to the use of probability-based filtering, sparse portfolio selection, and volatility-based risk scaling, which together create a more stable and robust trading strategy.

## Technologies

The project is implemented in Python using common data science and machine learning libraries. Data processing and feature construction are performed using Pandas and NumPy, while the predictive models are implemented using Scikit-learn. Visualization and analysis of results are carried out with Matplotlib.

## Repository Structure

The repository contains source code for feature engineering, model training, and backtesting, along with datasets, notebooks for experimentation, and a report describing the methodology and results. The project structure is organized to clearly separate data, implementation code, and documentation so that the workflow can be easily understood and reproduced.

## Author

Zahra Nazar Zadeh Attar

Collaborator: Amirali Askari [https://github.com/amiraliaskari2014]
