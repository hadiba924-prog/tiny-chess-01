# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/hadiba924-prog/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/hadiba924-prog/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

An original chess engine in under 4,096 bytes of Python, written from
scratch for the [make.fun "Build the strongest chess engine in 4 KB of
Python" bounty](https://make.fun/bounty/tiny-chess-01). No copied engine code; no model calls.

## How it plays

- 0x88 mailbox board, full legal move generation (castling, en passant,
  promotions) with lazy king-safety checks.
- Negamax alpha-beta with iterative deepening, a transposition table,
  killer moves and MVV-LVA move ordering.
- Quiescence search over captures and promotions, and over every reply
  while in check, so mates at the horizon are seen.
- Evaluation: material plus piece-square tables.
- Fully deterministic: a fixed 90,000-node budget per move, no wall
  clock, no unseeded randomness. A replay produces the same moves.

## Size

`main.py` is 3,673 bytes. The engine source is packed with zlib (base85)
to fit the 4,096-byte cap; the header comment of `main.py` says how to
unpack it. `LICENSE` is MIT, `README.md` is this file; the whole snapshot
is under the 8,192-byte cap and no file exceeds 4,096 bytes.

## Practice results

Local practice trials with the kit's env and official scorer:

- trial-0: Elo 1,191 — 2 wins, 1 draw, 3 losses (932 s). Wins against
  depth-2 and depth-3, a draw against depth-4.
- trial-1: Elo 876 — 0 wins, 2 draws, 4 losses (942 s).

## Grade locally

From the competition kit directory, with the entry repository at
`entry-repo/`:

    node cli/makefun.mjs grade-local --kit . --bot entry-repo --driver docker
