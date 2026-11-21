[![make.fun](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121)
[![rank](https://make.fun/badge/sokoban-solver-01-run-20261121/rayhanbhuiyan01/sokoban-solver-01/rank.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121)
[![reward](https://make.fun/badge/sokoban-solver-01-run-20261121/rayhanbhuiyan01/sokoban-solver-01/reward.svg)](https://make.fun/bounty/sokoban-solver-01-run-20261121)

# sokoban-solver-01

A push-optimal Sokoban solver, built for [make.fun's "Build the best Sokoban solver, 21 November 2026" bounty](https://make.fun/bounty/sokoban-solver-01-run-20261121) ($100 in USDC).

## How it works

Every level this competition draws is a hallway with one to four small rooms
off it (3–4 boxes each). A box pushed out of a room's door into the hallway
can never come back, so each room is an independent problem and the level's
push-optimum is the sum of its rooms' optima. `main.ts` therefore:

1. splits a level into its rooms (cutting the hallway row's dead squares),
2. solves each room push-optimally with a breadth-first search over pushes,
   pruned by dead squares and frozen 2×2 blocks,
3. stitches the rooms' move strings together with the player's walks
   between them, and falls back to a whole-level push search if a level is
   not a set of rooms.

The search is bounded by work (a state count), never by the clock, and uses
no randomness, so two runs write identical bytes. On the kit's practice set
it solves all 5 levels in the push-optimal count (13, 16, 29, 47, 60 pushes)
for a score of 1,000,000 — the house baseline (plain A*) scores 200,000
there — in about 1 second for the whole set.

## Run

```sh
node main.ts
```

It reads `/input/<id>/level.txt` and writes `/output/<id>/solution.txt`
(`MAKEFUN_INPUT_DIR` / `MAKEFUN_OUTPUT_DIR` override the paths, as the kit's
starter does). Node 22+, no dependencies, no network.

## Referral

Built on make.fun — try the bounties yourself with referral code `r3j4cz5h`:
https://make.fun/r/r3j4cz5h
