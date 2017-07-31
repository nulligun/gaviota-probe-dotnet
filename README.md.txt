This is a C# port of the Gaviota end game table base probing code. This is the same version of the probing code that is included in the Xbox version of Pwned the Game of Chess.

http://pwnedthegameofchess.com

How to use it

Add the EGTB project to your solution.
Add a reference for the EGTB's to your project.
Build the board structure and call the probing function
```

ProbeResultType probeResult = EGTB.Probe(whitePieceSquares, blackPieceSquares, whiteTypesSquares, blackTypesSquares, whosTurn, enPassantSquare);

if (probeResult.found) { if (probeResult.stm == MateResult.BlackToMate) { Console.WriteLine("Black to mate in {0} plies", pr.ply); } else if (probeResult.stm == MateResult.WhiteToMate) { Console.WriteLine("White to mate in {0} plies", pr.ply); } else if (probeResult.stm == MateResult.Draw) { Console.WriteLine("Draw", pr.ply); } else { Console.WriteLine("No match in EGTB", pr.ply); } } else { Console.WriteLine("Could not find it: " + pr.error); }

```

Board Structure

whitePieceSquares and blackPieceSquares are List<int> types. Each entry is a zero based index identifying the square that contains a piece. A1 is 0, A2 is 1 etc...

whiteTypeSquares and blackTypeSquares are List<int> types used to represent piece types for each square defined in the previous lists. There is an enum defined to map to the correct ID for each piece.

eg, for a white Rook at A1

whitePieceSquares = new List<int>(); whiteTypeSquares = new List<int>(); whitePieceSquares.Add(EGTB.A1); whiteTypeSquares.Add(EGTB.KING);

whosTurn 0 = white, 1 = black

enPassantSquare If a pawn has just made a two-square move, this is the position behind the pawn.

ProbeResultType

```

public bool found; // true if there was a hit public MateResult stm; // WhiteToMate, BlackToMate, Draw, Unknown public string error; // human readable error public int ply; // absolute distance to action public int dtm; // positive if we are mating, negative if being mated

```

For a complete example please see the egtb_probe solution. It will convert a FEN string to a Gaviota board structure and invoke the probing code.