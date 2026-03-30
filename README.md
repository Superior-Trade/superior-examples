# Superior Examples

Practical workflows and examples for using [Superior Trade](https://www.superior.trade/) through agents.

[Website](https://www.superior.trade/) · [Discord](https://discord.gg/aVZR8cCxcR) · [Twitter](https://x.com/SuperiorTrade_)

Designed for copy-paste usage, especially in OpenClaw-style environments where users want a fast path from prompt to structured trading workflow.

## Who this is for

- OpenClaw users
- Agent operators
- Prompt-first traders
- Developers testing strategy workflows through natural language

## Install the skill first

These examples require the Superior Trade skill. Install it using any of these methods:

**Prompt your agent:**

```
Get strategy trading skills from https://superior.trade/SKILL.md
```

**Or install from ClawHub:** [clawhub/superior-ai/superior-trade](https://clawhub.com/superior-ai/superior-trade)

**Or manually:** Copy the [`SKILL.md`](https://github.com/Superior-Trade/superior-skills/blob/main/SKILL.md) file into your agent's skill directory.

## How to use

Start with a narrow objective.

Good starting points:

- Backtest a BTC strategy using RSI
- Create a SOL breakout system with stop loss
- Run a low-volume altcoin short setup
- Define a trading workflow that always backtests before live deployment

Use the examples as templates and adapt them to your own pair, timeframe, and risk profile.

## Planned structure

```
superior-examples/
├── strategy_building/         # Strategy creation and backtesting workflows
│   ├── btc-rsi-backtest.md
│   ├── sol-breakout.md
│   └── hip3-stocks.md
└── autonomous_trading/        # Live deployment and agent operation workflows
    ├── deploy-and-monitor.md
    ├── contrarian-agent.md
    └── dca-workflow.md
```

## Philosophy

The goal is not theory. The goal is making it easy for users and agents to move from **idea → structured request → backtest-ready workflow**.

## Related

- [superior-skills](https://github.com/Superior-Trade/superior-skills) — The skill file and main documentation
- [superior-api](https://github.com/Superior-Trade/superior-api) — API documentation and test cases
- [superior-mcp](https://github.com/Superior-Trade/superior-mcp) — MCP integration layer
