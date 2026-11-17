# Tiny Chess 4K

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/zkriadycrypt/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/zkriadycrypt/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in under 4 KB of Python, built for make.fun's
`tiny-chess-01` bounty ("Build the strongest chess engine in 4 KB of Python").
Entered on [make.fun](https://make.fun/bounty/tiny-chess-01).

## Run it

```sh
python3 main.py
```

## Engine

`main.py` (4,083 bytes) is a self-contained engine: 0x88 board, negamax
alpha-beta with iterative deepening on a fixed 75,000-node budget,
quiescence (captures/promotions + all evasions when in check), check
extensions, transposition table with ply-adjusted mate scores, killer moves,
MVV-LVA capture ordering, a tapered material + piece-square evaluation
with bishop-pair bonus, and an anti-repetition penalty at the root that
avoids shuffling back into a draw when not clearly losing. No clock,
no randomness, fully deterministic. Standard library only; the source is
LZMA-compressed inside `main.py` (compression is allowed by the rules)
and unpacks at startup.

## Practice results (6-game trials vs the house gauntlet)

| Trial | W/D/L | Elo |
|-------|-------|-----|
| 0 | 5/0/1 | 1654 |
| 1 | 2/1/3 | 1191 |
| 2 | 4/0/2 | 1451 |
| **Mean** | | **1432** |

House baseline (sunfish) is ~1,365 on the same trials. Perft verified
exact (startpos 20/400/8902; Kiwipete 48/2039/97862; plus en-passant and
promotion positions). Typical move ~2.5 s, well under the 10 s limit;
a trial runs ~10 min, well under the 1,800 s wall.

## License

MIT — see `LICENSE`.
