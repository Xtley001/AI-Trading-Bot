# AI Trading Bot
This project implements an AI-powered trading bot that uses sentiment analysis from financial news to drive trading decisions. The bot integrates with Alpaca for live trading and Yahoo Finance for backtesting. It combines machine learning sentiment analysis using FinBERT and a dynamic position sizing strategy to make buy and sell decisions based on market sentiment and risk management.

## Features
1. Live Trading with Alpaca: Uses the Alpaca API for live trading, allowing for real-time market execution.
2. Sentiment Analysis: Leverages FinBERT to analyze sentiment from financial news headlines for stock symbols.
3. Position Sizing: Dynamically calculates position sizes based on available cash and predefined risk parameters.
4. Risk Management: Utilizes bracket orders to set take-profit and stop-loss levels, reducing risk exposure.
5. Backtesting with Yahoo Finance Data: Backtests strategies using historical stock data from Yahoo Finance to evaluate performance.

# Environment Configuration: Supports secure API key management via environment variables.

### Installation
### Prerequisites
1. Python 3.8 or higher
2. An Alpaca account with API access (for live trading)
3. A Yahoo Finance account for historical data (optional, for backtesting)
4. A .env file to store your API credentials

### Setup
Clone the repository:

git clone https://github.com/Xtley001/AI-Trading-Bot.git
cd AI-Trading-Bot

### Install required dependencies:

pip install -r requirements.txt
Create a .env file in the root directory with your Alpaca API credentials:

API_KEY=your_api_key
API_SECRET=your_api_secret
BASE_URL=https://paper-api.alpaca.markets

### Install additional dependencies:

1. lumibot: A lightweight Python library for backtesting trading strategies
2. finbert_utils: A utility library for sentiment analysis using FinBERT

### Configuration

In the MLTrader class, you can configure the following parameters:

1. symbol: The stock symbol to trade (default is "SPY").
2 cash_at_risk: The percentage of available cash to allocate per trade (default is 50%).

Example configuration for custom setup:

strategy = MLTrader(
    name='mlstrat',
    broker=broker,
    parameters={
        "symbol": "AAPL",
        "cash_at_risk": 0.5
    }
)

Strategy
The strategy consists of the following components:

1. Sentiment Analysis
The bot scrapes the latest news headlines for the specified stock symbol from Alpaca's news API.
It uses FinBERT, a pre-trained transformer model for financial sentiment analysis, to classify the sentiment as positive or negative.
If the sentiment is highly positive and the sentiment probability is greater than 99.9%, the bot buys the stock.
If the sentiment is negative and the sentiment probability is greater than 99.9%, the bot sells the stock.
2. Position Sizing
The bot calculates the amount of capital to risk based on the available cash and stock price. It determines the quantity of shares to buy or sell accordingly.
3. Risk Management
The bot uses bracket orders to place both a take-profit price and a stop-loss price for each trade. These levels are dynamically adjusted based on the latest price.
4. Trading Execution
Trades are executed through Alpaca’s paper trading API. The bot places market orders for buying and selling when the conditions are met.
5. Backtesting
The bot can be backtested using historical data from Yahoo Finance. You can adjust the start and end dates of the backtest.

Example:

start_date = datetime(2021, 12, 31)
end_date = datetime(2024, 11, 11)
broker = Alpaca(ALPACA_CREDS)
strategy = MLTrader(name='mlstrat', broker=broker,
                    parameters={"symbol": "SPY", 
                    "cash_at_risk": 0.5})
                    
strategy.backtest(YahooDataBacktesting, 
start_date, end_date, parameters={
"symbol":"SPY",
"cash_at_risk": 0.5})

Usage

Run the backtest with the following command:

code

python run_backtest.py

Start live trading (with Alpaca's paper trading mode):

python trading.py

The bot will automatically use financial news to inform trading decisions based on sentiment and will execute orders through Alpaca's API.

License

None.
