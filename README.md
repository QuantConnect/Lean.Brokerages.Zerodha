![header-cheetah](https://user-images.githubusercontent.com/79997186/184224088-de4f3003-0c22-4a17-8cc7-b341b8e5b55d.png)

&nbsp;
&nbsp;
&nbsp;

## Introduction

This repository hosts the Zerodha Brokerage Plugin Integration with the QuantConnect LEAN Algorithmic Trading Engine. LEAN is a brokerage agnostic operating system for quantitative finance. Thanks to open-source plugins such as this [LEAN](https://github.com/QuantConnect/Lean) can route strategies to almost any market.

[LEAN](https://github.com/QuantConnect/Lean) is maintained primarily by [QuantConnect](https://www.quantconnect.com), a US based technology company hosting a cloud algorithmic trading platform. QuantConnect has successfully hosted more than 200,000 live algorithms since 2015, and trades more than $1B volume per month.

### About Zerodha

<p align="center">
<picture >
  <source media="(prefers-color-scheme: dark)" srcset="https://zerodha.com/static/images/logo.svg">
  <source media="(prefers-color-scheme: light)" srcset="https://zerodha.com/static/images/logo.svg">
  <img alt="introduction" width="40%">
</picture>
<p>

[Zerodha](https://zerodha.com/) was founded by Nithin Kamath in 2010 with the goal to break all barriers that traders and investors face in India in terms of cost, support, and technology. Zerodha provides access to India Equities for clients in India with no minimum balance required. Zerodha also provides a mutual fund investment platform and an interactive portfolio dashboard.

For more information about the Zerodha brokerage, see the [QuantConnect-Zerodha Integration Page](https://www.quantconnect.com/docs/v2/our-platform/live-trading/brokerages/zerodha).

## Using the Brokerage Plugin
  
### Deploying Zerodha with VSCode User Interace

  You can deploy using a visual interface in the QuantConnect cloud. For instructions, see the [QuantConnect-Zerodha brokerage Integration Page](https://www.quantconnect.com/docs/v2/our-platform/live-trading/brokerages/zerodha). 
  
  ![deploy-zerodha](https://user-images.githubusercontent.com/38889814/188248274-e9801f4b-ec42-4b05-bba4-77b1ad58ba93.gif)

  In the QuantConnect Cloud Platform, you can harness the QuantConnect Live Data Feed. For most users, this is substantially cheaper and easier than self-hosting.
  
### Deploying Zerodha with LEAN CLI

Follow these steps to start local live trading with the Zerodha brokerage:

1.  Open a terminal in your [CLI root directory](https://www.quantconnect.com/docs/v2/lean-cli/initialization/directory-structure#02-lean-init).
2.  Run `lean live "<projectName>`" to start a live deployment wizard for the project in ./`<projectName>` and then enter the brokerage number.

    ```
    $ lean live 'My Project'
     
    Select a brokerage:
    1. Paper Trading
    2. Interactive Brokers
    3. Tradier
    4. Oanda
    5. Bitfinex
    6. Coinbase Pro
    7. Binance
    8. Zerodha
    9. Samco
    10. Terminal Link
    11. Atreyu
    12. Trading Technologies
    13. Kraken
    14. FTX
    Enter an option: 
    ```
  
3.  Enter the number of the organization that has a subscription for the Zerodha module.

    ```
    $ lean live "My Project" 

    Select the organization with the Zerodha module subscription:
    1. Organization 1
    2. Organization 2
    3. Organization 3
    Enter an option: 1
    ```

4.  Enter your Zerodha credentials.

    ```
    $ lean live "My Project" 
    Your Kite Connect API key
    API key:
    Your Kite Connect access token
    Access token:
    ```

5.  Enter your Zerodha product type.

    ``` 
    $ lean live "My Project"

    The product type must be set to MIS if you are targeting intraday products, CNC if you are targeting delivery products
    or NRML if you are targeting carry forward products.
    Product type (mis, cnc, nrml) [mis]:
    ```

6.  Enter your Zerodha trading segment.

    ``` 
    $ lean live "My Project"

    The trading segment must be set to EQUITY if you are trading equities on NSE or BSE, or COMMODITY if you are trading
    commodities on MCX.
    Trading segment (equity, commodity) [equity]:
    ```

7.  Enter if you have a history API subscription of Zerodha.

    ``` 
    $ lean live "My Project"

    Do you have a history API subscription? [False]:
    ```

8.  Enter the number of the data feed to use and then follow the steps required for the data connection.

    ``` 
    $ lean live 'My Project'

    Select a data feed:
    1. Interactive Brokers
    2. Tradier
    3. Oanda
    4. Bitfinex
    5. Coinbase Pro
    6. Binance
    7. Zerodha
    8. Samco
    9. Terminal Link
    10. Trading Technologies
    11. Kraken
    12. FTX
    13. IQFeed
    14. Polygon Data Feed
    15. Custom Data Only

    To enter multiple options, separate them with comma:
    ```

9. View the result in the `<projectName>/live/<timestamp>` directory. Results are stored in real-time in JSON format. You can save results to a different directory by providing the `--output <path>` option in step 2.

If you already have a live environment configured in your [Lean configuration file](https://www.quantconnect.com/docs/v2/lean-cli/initialization/configuration#03-Lean-Configuration), you can skip the interactive wizard by providing the `--environment <value>` option in step 2. The value of this option must be the name of an environment which has `live-mode` set to true.

## Account Types

Zerodha supports cash and margin accounts that trades in Indian Rupees.

## Order Types and Asset Classes


Zerodha supports trading India Equities with the following order types:

- Market Order
- Limit Order
- Limit-If-Touch Order
- Stop-Market Order
- Stop-Limit Order
- Market-On-Open Order
- Market-On-Close Order


## Downloading Data

For local deployment, the algorithm needs to download the following dataset:

- [India Equities](https://www.quantconnect.com/datasets/truedata-india-equities) provided by TrueData
- [India Equity Security Master](https://www.quantconnect.com/datasets/truedata-india-equity-security-master) provided by TrueData


## Brokerage Model

Lean models the brokerage behavior for backtesting purposes. The margin model is used in live trading to avoid placing orders that will be rejected due to insufficient buying power.

You can set the Brokerage Model with the following statements
```
SetBrokerageModel(BrokerageName.Zerodha, AccountType.Cash);
SetBrokerageModel(BrokerageName.Zerodha, AccountType.Margin);
```

[Read Documentation](https://www.quantconnect.com/docs/v2/our-platform/live-trading/brokerages/zerodha)

### Fees

We model the order fees of Zerodha with its Equity Intraday fee structure. The following table shows the fees:

| Charge Item | Fee |
| --- | --- |
| Brokerage Fee | ₹20 per trade or 0.03% (whichever is lower) |
| Exchange Transaction Charge | 0.00345% |
| Securities Transaction Tax | 0.025% |
| Goods and Services Tax | 18% |
| SEBI Charges | 0.0001% |
| Stamp Duty | 0.003% |

To check the latest fees, see the [Charges page](https://zerodha.com/charges#tab-equities) on the Zerodha website.

### Margin

We model buying power and margin calls to ensure your algorithm stays within the margin requirements.

[Read Documentation](https://www.quantconnect.com/docs/v2/our-platform/live-trading/brokerages/zerodha)

#### Buying Power

Zerodha allows up to 5x leverage for margin accounts, but the amount of margin available depends on the Equity and product type. To check the amount of margin available for each asset, see the [Margin Calculator](https://zerodha.com/margin-calculator/Equity/) on the Zerodha website.

#### Margin Calls

Regulation T margin rules apply. When the amount of margin remaining in your portfolio drops below 5% of the total portfolio value, you receive a [warning](https://www.quantconnect.com/docs/v2/writing-algorithms/reality-modeling/margin-calls#08-Monitor-Margin-Call-Events). When the amount of margin remaining in your portfolio drops to zero or goes negative, the portfolio sorts the generated margin call orders by their unrealized profit and executes each order synchronously until your portfolio is within the margin requirements.

### Slippage

Orders through Zerodha do not experience slippage in backtests. In live trading, your orders may experience slippage.

### Fills

We fill market orders immediately and completely in backtests. In live trading, if the quantity of your market orders exceeds the quantity available at the top of the order book, your orders are filled according to what is available in the order book.

### Settlements

If you trade with a margin account, trades settle immediately. If you trade with a cash account, Equity trades settle 3 days after the transaction date (T+3).

### Deposits and Withdraws

You can deposit and withdraw cash from your brokerage account while you run an algorithm that's connected to the account. We sync the algorithm's cash holdings with the cash holdings in your brokerage account every day at 7:45 AM Eastern Time (ET).

&nbsp;
&nbsp;
&nbsp;

![whats-lean](https://user-images.githubusercontent.com/79997186/184042682-2264a534-74f7-479e-9b88-72531661e35d.png)

&nbsp;
&nbsp;
&nbsp;

LEAN Engine is an open-source algorithmic trading engine built for easy strategy research, backtesting, and live trading. We integrate with common data providers and brokerages, so you can quickly deploy algorithmic trading strategies.

The core of the LEAN Engine is written in C#, but it operates seamlessly on Linux, Mac and Windows operating systems. To use it, you can write algorithms in Python 3.8 or C#. QuantConnect maintains the LEAN project and uses it to drive the web-based algorithmic trading platform on the website.

## Contributions

Contributions are warmly very welcomed but we ask you to read the existing code to see how it is formatted, commented and ensure contributions match the existing style. All code submissions must include accompanying tests. Please see the [contributor guide lines](https://github.com/QuantConnect/Lean/blob/master/CONTRIBUTING.md).

## Code of Conduct

We ask that our users adhere to the community [code of conduct](https://www.quantconnect.com/codeofconduct) to ensure QuantConnect remains a safe, healthy environment for
high quality quantitative trading discussions.

## License Model

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You
may obtain a copy of the License at

<http://www.apache.org/licenses/LICENSE-2.0>

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language
governing permissions and limitations under the License.
