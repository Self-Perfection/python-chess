Variants (experimental)
=======================

python-chess supports several chess variants.

>>> import chess.variant
>>> board = chess.variant.GiveawayBoard()

>>> # General information about the variants
>>> type(board).uci_variant
'giveaway'
>>> type(board).starting_fen
'rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w - - 0 1'

>>> # Check for special variant game-end conditions
>>> board.is_variant_win()
False
>>> board.is_variant_draw()
False
>>> board.is_variant_loss()
False

================ ========================================= ============= ============
Variant          Board class                               UCI           Syzygy
================ ========================================= ============= ============
Standard         :class:`chess.Board`                      chess         .rtbw, .rtbz
Suicide          :class:`chess.variant.SuicideBoard`       suicide       .stbw, .stbz
Giveaway         :class:`chess.variant.GiveawayBoard`      giveaway      .gtbw, .gtbz
Atomic           :class:`chess.variant.AtomicBoard`        atomic        .atbw, .atbz
King of the Hill :class:`chess.variant.KingOfTheHillBoard` kingofthehill
Racing Kings     :class:`chess.variant.RacingKingsBoard`   racingkings
Horde            :class:`chess.variant.HordeBoard`         horde
Three-check      :class:`chess.variant.ThreeCheckBoard`    threecheck
Crazyhouse       :class:`chess.variant.CrazyhouseBoard`    crazyhouse
================ ========================================= ============= ============

.. autofunction:: chess.variant.find_variant

Chess960
--------

Chess960 is orthogonal to all other variants.

>>> chess.Board(chess960=True)
Board('rnbqkbnr/pppppppp/8/8/8/8/PPPPPPPP/RNBQKBNR w KQkq - 0 1', chess960=True)

UCI
---

Stockfish and other engines allow you to switch variants by setting the
``UCI_Variant`` option.

>>> board = chess.variant.RacingKingsBoard()
>>> engine.setoption({
...     "UCI_Variant": type(board).uci_variant,
...     "UCI_Chess960": board.chess960
... })
>>> engine.position(board)

Syzygy
------

Syzygy tablebases are available for suicide, giveaway and atomic chess.

>>> tables = chess.syzygy.open_tablebases("data/syzygy", VariantBoard=chess.variant.AtomicBoard)
