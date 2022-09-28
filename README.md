# Lichess Combined Puzzle-Game Database
The Lichess puzzle database joined with game information.

## Background

This contains every puzzle from the [Lichess Puzzle Database](https://database.lichess.org/#puzzles) joined with their games from the [Lichess Game Database](https://database.lichess.org/#standard_games). The puzzle data was pulled in August 2022 and will be updated periodically. There are 2,834,182 puzzles in total. The game info was pulled from the [Lichess API](https://lichess.org/api) with [every flag enabled](https://lichess.org/api#tag/Games/operation/gamesExportIds).

## Format
The files are compressed with `bzip2`. There are 15 files in total, numbered `01` to `15`. Each file contains 200,000 games, except the last one, which contains 34,182. The entries are not guaranteed to be ordered in any specific way. The uncompressed data is around 6.5GB.

The files are in [`ndjson` format](http://ndjson.org/), with one JSON object on each line. Each top-level JSON object contains two fields: `game` and `puzzle`. The `game` object contains the entire JSON dump of the game information from the [Lichess API call](https://lichess.org/api#tag/Games/operation/gamesExportIds) with every flag enabled. The `puzzle` object contains all of the information from the puzzle database entry, with the field names being taken from the [csv headers](https://database.lichess.org/#puzzles). That is, you can expect the following fields in the `puzzle` object (though they are not necessarily all populated): `PuzzleId`,`FEN`,`Moves`,`Rating`,`RatingDeviation`,`Popularity`,`NbPlays`,`Themes`,`GameUrl`,`OpeningFamily`, and `OpeningVariation`.

The games and puzzles are joined by the game id (`id` in the `game` object). The matching `id` is extracted from a puzzle's `GameUrl` field. Note that `PuzzleId` has a different meaning.

## Example
```
{"puzzle":{"Themes":"crushing kingsideAttack long middlegame pin","OpeningFamily":"","Popularity":"100","NbPlays":"1","PuzzleId":"002rd","FEN":"r6k/q1pb1p1p/1b3Pr1/p1ppP2Q/3P2p1/4B3/PP2NRPP/3R2K1 b - - 1 25","Moves":"d7e6 e2f4 c5d4 f4g6 f7g6 h5h6","Rating":"1500","RatingDeviation":"500","GameUrl":"https://lichess.org/NcD6lul8/black#50"},"game":{"createdAt":1652296484864,"variant":"standard","status":"resign","pgn":"[Event \"Rated Blitz game\"]\n[Site \"https://lichess.org/NcD6lul8\"]\n[Date \"2022.05.11\"]\n[White \"morteza0521\"]\n[Black \"salirbeber\"]\n[Result \"1-0\"]\n[UTCDate \"2022.05.11\"]\n[UTCTime \"19:14:44\"]\n[WhiteElo \"2164\"]\n[BlackElo \"2270\"]\n[WhiteRatingDiff \"+7\"]\n[BlackRatingDiff \"-7\"]\n[Variant \"Standard\"]\n[TimeControl \"180+0\"]\n[ECO \"C44\"]\n[Opening \"Scotch Game: Scotch Gambit, Advance Variation\"]\n[Termination \"Normal\"]\n[Annotator \"lichess.org\"]\n\n1. e4 e5 2. Nf3 Nc6 3. d4 exd4 4. Bc4 Nf6 5. e5 { C44 Scotch Game: Scotch Gambit, Advance Variation } d5 6. Bb5 Ne4 7. Nxd4 Bd7 8. Bxc6 bxc6 9. O-O Bc5 10. c3 O-O 11. f3 Ng5 12. f4 Ne6 13. Be3 Nxd4 14. cxd4 Bb6 15. f5 a5 16. f6 g6 17. Qf3 Kh8 18. Qf4 Qb8 19. Qh6 Rg8 20. Rf4 g5 21. Rf2 Rg6 22. Qh5 g4 23. Nc3 Qa7 24. Rd1 c5 25. Ne2 Be6 26. Nf4 Rag8 27. Nxe6 fxe6 28. f7 Rf8 29. Bh6 cxd4 30. Bxf8 d3 31. Bg7+ { Black resigns. } 1-0\n\n\n","id":"NcD6lul8","clock":{"increment":0,"totalTime":180,"initial":180},"rated":true,"players":{"white":{"rating":2164,"user":{"name":"morteza0521","id":"morteza0521"},"ratingDiff":7},"black":{"rating":2270,"user":{"name":"salirbeber","id":"salirbeber"},"ratingDiff":-7}},"winner":"white","moves":"e4 e5 Nf3 Nc6 d4 exd4 Bc4 Nf6 e5 d5 Bb5 Ne4 Nxd4 Bd7 Bxc6 bxc6 O-O Bc5 c3 O-O f3 Ng5 f4 Ne6 Be3 Nxd4 cxd4 Bb6 f5 a5 f6 g6 Qf3 Kh8 Qf4 Qb8 Qh6 Rg8 Rf4 g5 Rf2 Rg6 Qh5 g4 Nc3 Qa7 Rd1 c5 Ne2 Be6 Nf4 Rag8 Nxe6 fxe6 f7 Rf8 Bh6 cxd4 Bxf8 d3 Bg7+","opening":{"name":"Scotch Game: Scotch Gambit, Advance Variation","eco":"C44","ply":9},"perf":"blitz","speed":"blitz","lastMoveAt":1652296756535}}
```

## License

This is under a Creative Commons Zero v1.0 Universal License, in line with how Lichess releases the data.

## Errors/Refreshes

Please feel free open an issue if you find any errors or if you find that the database is very out-of-date.
