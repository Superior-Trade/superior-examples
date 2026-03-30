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

## Strategy Building

| Prompt | Description | Link |
|--------|-------------|------|
| S&P 500 DCA | Dollar-cost averaging strategy on the S&P 500 index via Hyperliquid HIP3 | [s&p500-dca.md](strategy_building/s&p500-dca.md) |

## Autonomous Trading

| Prompt | Description | Link |
|--------|-------------|------|
| Contrarian Agent | Self-learning contrarian trading agent with journal-based memory and twice-daily scheduling | [contrarian-agent.md](autonomous_trading/contrarian-agent.md) |
| Nansen Smart Money Signal | Signal-driven agent that scores Nansen smart money flow, picks the highest-conviction pair, and auto-rotates every 4 hours | [nansen-smart-money.md](autonomous_trading/nansen-smart-money.md) |

## Miscellaneous

| Prompt | Description | Link |
|--------|-------------|------|
| Multi-Account Management | Manage multiple Superior Trade accounts from a single agent session | [multi-account.md](miscellaneous/multi-account.md) |

## Philosophy

The goal is not theory. The goal is making it easy for users and agents to move from **idea → structured request → backtest-ready workflow**.

## Related

- [superior-skills](https://github.com/Superior-Trade/superior-skills) — The skill file and main documentation
- [superior-api](https://github.com/Superior-Trade/superior-api) — API documentation and test cases
- [superior-mcp](https://github.com/Superior-Trade/superior-mcp) — MCP integration layer
