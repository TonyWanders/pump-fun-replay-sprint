# Sieve — Pump.fun Replay Sprint bot
[![make.fun](https://make.fun/badge/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122.svg)](https://make.fun/bounty/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122)
[![rank](https://make.fun/badge/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122/TonyWanders/pump-fun-replay-sprint/rank.svg)](https://make.fun/bounty/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122/leaderboard)
[![reward](https://make.fun/badge/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122/TonyWanders/pump-fun-replay-sprint/reward.svg)](https://make.fun/bounty/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122)

Paper-trading bot for the [Pump.fun Replay Sprint — Paper Bot, Real Ranking](https://make.fun/bounty/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122) bounty ($2, 3 places). It trades 10 SOL of paper money on a 24h pump.fun replay, scored on net PnL after every fee. A placement needs net PnL above holding cash (above 0).

## Strategy

Sieve watches every new bonding curve for its first minutes and buys only the coins where real buyers are piling in hard: at least 10 distinct buyers and 10 buy trades with 5 SOL net inflow inside a 240-slot window, buys dominating sells, price already up 5% to 80% from first sight, real SOL reserves above 1.5 SOL, coin younger than 900 slots. One fixed 0.05 SOL stake per coin, one shot per coin, at most 5 positions open.

Exits, whichever comes first: take-profit +15%, stop-loss -6%, trailing exit (arms at +12%, fires on a 6% pullback off the peak), or a 240-slot time exit.

## Entry point

`main.py` (Python 3.13, standard library only). The grader runs it as `python3 -P -s /bot/main.py` with `PYTHONHASHSEED=0`. It speaks agent-fun/replay/v2 through the kit's Python shim in `vendor/makefun_bot.py`. All decisions use integer math on lamports and slot counts only: no floats, no clock, no environment, no randomness, so two executions produce byte-identical action logs.

## Files

- `main.py` — the strategy (entry point)
- `vendor/makefun_bot.py` — the kit's Python protocol shim, copied from the kit's `sdk/python` as its docstring instructs
- `muse-usage-pump-fun-replay-sprint.jsonl` — token usage rows for this build session
- `LICENSE` — MIT

## Bounty

- Page: https://make.fun/bounty/u-jackxyz72-pump-fun-replay-sprint-paper-bot-0b809122
- Reward: $2 (1st $1, 2nd $0.60, 3rd $0.40), escrowed on Solana
- Ends Fri 27 Nov 2026 05:50 WAT; Round 1 closes Mon 24 Nov 2026 21:50 WAT
- Guardrails: at least 20 coins with round trips of 0.01 SOL or more, max drawdown 50% or less
