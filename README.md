# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/jackdems/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/jackdems/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 3,639 bytes of Python. `main.py` is the whole engine: an
alpha-beta negamax search with a capture-only quiescence search at the leaves
and piece-square evaluation, run to a fixed node budget so a replay plays the
same moves. Entered in make.fun's [Build the strongest chess engine in 4 KB of
Python](https://make.fun/bounty/tiny-chess-01) bounty.

## Run it

```
MAKEFUN_ENV_URL=http://127.0.0.1:8080 python3.13 main.py
```

The engine speaks to the env at `MAKEFUN_ENV_URL`: it asks `/game` for the game
in play, picks a move from the `legal_moves` the env hands it, and posts it to
`/move`. It reads, imports and execs no other file.

## How it plays

- **Search.** Negamax alpha-beta over a budget of 64,000 nodes a move, with
  iterative deepening from depth 1. The budget is counted inside the search and
  quiescence, so it stops mid-tree instead of after a whole depth, and a depth
  cut short is dropped in favour of the last one that finished.
- **Quiescence.** At the leaves it searches captures only, so it does not stop
  counting in the middle of an exchange.
- **Evaluation.** Material plus piece-square tables, from white's side, negated
  for black.
- **Determinism.** It searches to a fixed node count, never to a clock, and
  seeds nothing, so two runs on the same data play the same moves. Move ordering
  is a stable sort, so equal-scoring moves keep the env's order.

## The size rule

`main.py` is at most 4,096 bytes as committed; this repository is at most 8,192
bytes in all. It is packed with the kit's `compress` command from a readable
source of the same engine. Python 3.13, standard library only.

## Grade it locally

Download the competition's dev kit, unpack it, and from inside it run:

    node cli/makefun.mjs grade-local --kit . --bot <your repository>

## License

MIT.
