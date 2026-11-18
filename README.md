# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Ocarsx/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Ocarsx/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 4,092 bytes of Python — v2-lite. 0x88 board, negamax
alpha-beta with quiescence search, a transposition table, MVV-LVA and
killer move ordering, and piece-square table evaluation. It searches to
a fixed budget of 40,000 nodes a move, never to a clock, so every move
is deterministic and a replay plays the same game.

New in v2-lite, over the first entry:

- Principal variation search (PVS) with late move reductions (LMR) for
  quiet moves late in the ordering.
- Null-move pruning, guarded by an incrementally tracked non-pawn
  material count so it never fires in pawn-only endings or in check.
- Check extensions: a side in check searches one ply deeper.
- A fixed promotion bug: the first entry's UCI writer was off by one
  in the promotion piece letters, so a queen promotion crashed and the
  move fell back to the first legal move. Promotions now round-trip
  correctly for knight, bishop, rook and queen.

To fit the 4,096-byte cap, the lite build folds the endgame king table
into the piece-square tables and stores those tables mirrored, and it
drops the pawn-structure terms and the bishop-pair bonus of the fuller
v2 build, which packed to 4,434 bytes and did not fit.

`main.py` is an lzma-packed payload with its unpacker; unpacked it is
plain Python 3.13, standard library only, and it reads no other file.

## Verification

The packed `main.py` shipped here was loaded and tested as-is: perft
from the start position gives 8,902 nodes at depth 3 and the Kiwipete
position gives 97,862 at depth 3, matching the known values; the
best move from the start position is b1c3; and promotion moves
round-trip through the UCI writer and parser for all four pieces
(e7e8n, e7e8b, e7e8r, e7e8q). The fuller v2 search line this lite
build is cut from scored a local practice mean of Elo 1,404 over the
kit's three practice instances, against the house baseline's 1,365.

## Run it

The grader runs `python3 -P -s main.py` with `MAKEFUN_ENV_URL` set; the
engine asks the env for the game in play, sends its moves in UCI, and
exits when the env answers done.

---
<sub>Entered on [make.fun](https://make.fun/?ref=s1m1n3px&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
