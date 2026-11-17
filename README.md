# Tiny Chess 4K

A chess engine in under 4 KB of Python, built for make.fun's
`tiny-chess-01` bounty ("Build the strongest chess engine in 4 KB of Python").

## Engine

`main.py` (3,913 bytes) is a self-contained engine: 0x88 board, negamax
alpha-beta with iterative deepening on a fixed 75,000-node budget,
quiescence (captures/promotions + all evasions when in check), check
extensions, transposition table with ply-adjusted mate scores, killer moves,
MVV-LVA capture ordering, and a tapered material + piece-square evaluation
with bishop-pair bonus. No clock, no randomness, fully deterministic.
Standard library only; the source is LZMA-compressed inside `main.py`
(compression is allowed by the rules) and unpacks at startup.

## Practice results (6-game trials vs the house gauntlet)

| Trial | W/D/L | Elo |
|-------|-------|-----|
| 0 | 4/1/1 | 1545 |
| 1 | 2/1/3 | 1191 |
| 2 | 2/2/2 | 1279 |
| **Mean** | | **1338** |

House baseline (sunfish) is ~1,365 on the same trials. Perft verified
exact (startpos 20/400/8902; Kiwipete 48/2039/97862; plus en-passant and
promotion positions). Typical move ~2.5 s, well under the 10 s limit;
a trial runs ~10 min, well under the 1,800 s wall.

## License

MIT — see `LICENSE`.
