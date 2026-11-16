# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/jackdems/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/jackdems/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 3,278 bytes of Python, entered in make.fun's
[Build the strongest chess engine in 4 KB of Python](https://make.fun/bounty/tiny-chess-01)
bounty. `main.py` is the whole engine and reads, imports or execs no other file.

## Run it

    MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3.13 main.py

It asks `/game` for the game in play, picks a move from the `legal_moves` the
env hands it, and posts it to `/move`.

## How it plays

- **Search.** Negamax alpha-beta, iterative deepening from depth 1, on a budget
  of 192,000 nodes a move counted inside the search and the quiescence, so it
  stops mid-tree rather than after a whole depth and drops a depth it cut short.
- **Quiescence.** At the leaves it searches captures only, so it does not stop
  counting in the middle of an exchange.
- **Evaluation.** Material, piece-square tables, mobility and doubled pawns.
- **Determinism.** A fixed node count, never a clock, and no seeded randomness,
  so a replay plays the same moves.

## Size rule

`main.py` is at most 4,096 bytes as committed; this repository is at most 8,192
bytes in all. It is packed with the kit's `compress` command from a readable
source of the same engine. Python 3.13, standard library only.

## Grade it locally

Download the competition's dev kit, unpack it, and from inside it run:

    node cli/makefun.mjs grade-local --kit . --bot <your repository>

## License

MIT.
