# Tiny Chess — tiny-chess-01

[![make.fun bounty](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/at79x/tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/at79x/tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01)

An original chess engine in 4 KB of Python for the [tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01) ($500 USDC).

## The engine

`main.py` (3,651 bytes) is the whole engine: a zlib+base64 compressed payload
that unpacks and execs the readable engine (Python 3.13, stdlib only; it
reads, imports or execs no other repo file). The readable source is kept
outside the repo for reference.

- 0x88 board, negamax alpha-beta with iterative deepening to a fixed
  100,000-node budget per move (never a clock — deterministic).
- Move ordering: transposition-table move, killers, history, MVV-LVA captures.
- Quiescence on captures with delta pruning; full evasions when in check.
- Transposition table (EXACT/LOWER/UPPER), killer moves, history heuristic.
- Original evaluation: material, pawn advance + 6th/7th-rank bonus, pawn
  structure (isolated/doubled), rook open/semi-open files, piece centrality,
  bishop pair, king safety (back-rank bonus, endgame centralisation,
  pawn shelter).
- Full rules: castling, en passant, promotion to queen; mate/stalemate
  handled in search. No opening book, no tablebase, no model calls.

Practice (sealed scorer, 6 games each): trial-0 Elo 1279, trial-1 Elo 1451,
trial-2 Elo 1191 (18-game mean ≈ 1307).
