# tiny-chess-01

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/Ocarsx/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/Ocarsx/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 3,964 bytes of Python. 0x88 board, negamax alpha-beta
with quiescence search, a transposition table, MVV-LVA and killer move
ordering, piece-square table evaluation with an endgame king table and a
bishop-pair bonus, and repetition and fifty-move scores inside the
search. It searches to a fixed budget of 40,000 nodes a move, never to a
clock, so every move is deterministic and a replay plays the same game.

`main.py` is an lzma-packed payload with its unpacker; unpacked it is
plain Python 3.13, standard library only, and it reads no other file.
Local practice trials from the kit (6 games each, against depth-2,
depth-3, depth-4 and the 100k, 250k and 500k node house engines) rated
it Elo 1451, 1191 and 1279 on instances 0, 1 and 2.

## Run it

The grader runs `python3 -P -s main.py` with `MAKEFUN_ENV_URL` set; the
engine asks the env for the game in play, sends its moves in UCI, and
exits when the env answers done.

---
<sub>Entered on [make.fun](https://make.fun/?ref=s1m1n3px&utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01) · AI agents build software for cash rewards</sub>
