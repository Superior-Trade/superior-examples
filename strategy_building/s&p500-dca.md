# S&P 500 DCA Strategy

<!--
  Drop this file's raw URL into any AI agent to build and backtest
  a dollar-cost averaging strategy on the S&P 500 index via Hyperliquid HIP3.

  Requires the Superior Trade skill:
  https://github.com/Superior-Trade/superior-skills
-->

Build a dollar-cost averaging (DCA) strategy that trades the S&P 500 index on Hyperliquid using the Superior Trade API. Follow these instructions for the rest of this session.

## Skill check

Before doing anything else, confirm the Superior Trade skill is loaded. If it is not, fetch and install it from:

```
https://superior.trade/SKILL.md
```

## What you are building

A long-only DCA strategy on the S&P 500 perpetual contract. The strategy enters on dips and adds to the position when price drops further, averaging down the entry price.

**Pair:** `XYZ-SP500/USDC:USDC`
**Protocol:** XYZ (HIP3 tokenized real-world asset on Hyperliquid)
**Trading mode:** futures, isolated margin (required for all HIP3 assets)
**Stake currency:** USDC

> **Data availability note:** S&P 500 was listed on Hyperliquid on March 18, 2026. Backtest data may be limited. If backtesting fails with "No data found", use `XYZ-AAPL/USDC:USDC` as a proxy to validate the strategy, then switch back to SP500 for deployment.

## Strategy spec

### Entry logic

- Price is above the 50-period SMA (uptrend filter)
- RSI(14) is below 40 (buying the dip within an uptrend)

### DCA logic

- When an open trade drops more than 3% from entry, add another $50 (or `min_stake`, whichever is greater)
- This requires `position_adjustment_enable = True` in the strategy class

### Exit logic

- RSI(14) crosses above 75 (momentum exhaustion)
- Minimal ROI: 10% immediate target
- Stoploss: -10%

### Config

```json
{
  "exchange": {
    "name": "hyperliquid",
    "pair_whitelist": ["XYZ-SP500/USDC:USDC"]
  },
  "stake_currency": "USDC",
  "stake_amount": 50,
  "timeframe": "15m",
  "max_open_trades": 1,
  "stoploss": -0.10,
  "trading_mode": "futures",
  "margin_mode": "isolated",
  "minimal_roi": { "0": 0.10 },
  "entry_pricing": { "price_side": "other" },
  "exit_pricing": { "price_side": "other" },
  "pairlists": [{ "method": "StaticPairList" }]
}
```

### Strategy code

```python
from freqtrade.strategy import IStrategy
import pandas as pd
import talib.abstract as ta


class SP500DCAStrategy(IStrategy):
    minimal_roi = {"0": 0.10}
    stoploss = -0.10
    trailing_stop = False
    timeframe = '15m'
    process_only_new_candles = True
    startup_candle_count = 50
    position_adjustment_enable = True

    def populate_indicators(self, dataframe: pd.DataFrame, metadata: dict) -> pd.DataFrame:
        dataframe['sma_50'] = ta.SMA(dataframe, timeperiod=50)
        dataframe['rsi'] = ta.RSI(dataframe, timeperiod=14)
        return dataframe

    def populate_entry_trend(self, dataframe: pd.DataFrame, metadata: dict) -> pd.DataFrame:
        dataframe.loc[
            (dataframe['close'] > dataframe['sma_50']) &
            (dataframe['rsi'] < 40),
            'enter_long'
        ] = 1
        return dataframe

    def populate_exit_trend(self, dataframe: pd.DataFrame, metadata: dict) -> pd.DataFrame:
        dataframe.loc[(dataframe['rsi'] > 75), 'exit_long'] = 1
        return dataframe

    def adjust_trade_position(self, trade, current_time, current_rate,
                              current_profit, min_stake, max_stake,
                              current_entry_rate, current_exit_rate,
                              current_entry_profit, current_exit_profit, **kwargs):
        if current_profit < -0.03:
            return max(50, min_stake)
        return None
```

## Workflow

1. **Backtest first.** Create a backtest with the config, code, and a timerange covering recent data. If SP500 data is unavailable, substitute `XYZ-AAPL/USDC:USDC` in the pair whitelist to validate.
2. **Review results.** Check total trades, win rate, profit, max drawdown. A DCA strategy on a trending asset should show moderate trade counts with averaged-down entries.
3. **Adjust if needed.** Tune the RSI entry threshold (try 35 or 45), the DCA trigger (-0.03 → -0.02 or -0.05), or the timeframe (try 1h for longer holds).
4. **Deploy.** Once satisfied, create a deployment with the SP500 pair. Remember: HIP3 assets may have reduced liquidity outside US market hours.

## Customization ideas

- **Multi-pair DCA:** Add more HIP3 indices to the pair whitelist (e.g. `XYZ-JP225/USDC:USDC` for Nikkei 225)
- **Tighter DCA:** Lower the -3% threshold to -1.5% for more frequent averaging
- **Trailing stop:** Enable `trailing_stop = True` with `trailing_stop_positive = 0.03` to lock in gains on momentum moves
- **Longer timeframe:** Switch to 1h or 4h for a less active, more swing-oriented version
