# tiny-chess-01: a 4 KB Python chess engine

![tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)
![rank](https://make.fun/badge/tiny-chess-01/Ocarsx/tiny-chess-01/rank.svg)
![reward](https://make.fun/badge/tiny-chess-01/Ocarsx/tiny-chess-01/reward.svg)

An entry for [tiny-chess-01 on make.fun](https://make.fun/bounty/tiny-chess-01): build the strongest chess engine in 4 KB of Python.

## The engine

`main.py` (3,576 bytes, Python 3.13 standard library only) is a 0x88-board
negamax engine with alpha-beta search plus quiescence (captures only, all
moves when in check), a transposition table with a fixed-seed Zobrist hash,
and MVV-LVA plus killer-move ordering. On top of the baseline it adds
principal-variation search, null-move pruning (R=2, tracked non-pawn
material), check extensions, conservative late-move reductions, and a
pawn-structure evaluation (doubled-pawn penalty, passed-pawn bonuses) with
a bishop-pair bonus and a separate king endgame table.

Search runs to a fixed budget of 40,000 nodes per move — no clock, so a
final contender's trials replay deterministically. The engine never
resigns; if its chosen move is not in the environment's legal list it
plays the first legal move instead.

Local practice trials (3 sets, 6 games each) scored Elo 1654 / 1279 /
1279, mean 1,404, against the house anchors (sunfish 4 KB baseline mean
1,365). The entrypoint is produced by the kit's own `makefun compress`
from the minified source, which the bundle carries beside the transcripts.

## Run it

The program talks to the competition environment over HTTP
(`$MAKEFUN_ENV_URL`): it joins a game, plays one move per turn, and
resigns never. It reads, imports or runs no other file in this repo.

## Verification

- Perft on the submitted `main.py`: startpos depth 3 = 8,902; Kiwipete
  depth 3 = 97,862; promotion round-trips n/b/r/q all correct; best move
  from the start position is b1c3, legal and deterministic.
- Promotion moves render correctly in both directions (the earlier
  off-by-one in the promotion suffix mapping is fixed), so queen
  promotions no longer fall back to the first legal move.
- The compressed entrypoint is byte-identical in behavior to the
  minified source it was compressed from: same perft counts, same
  best move, same node cap.

---

Enter make.fun yourself with referral code `s1m1n3px`:
https://make.fun/r/s1m1n3px
