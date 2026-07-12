# ♜ @mady9613/chess-engine

<div align="center">

[![npm version](https://img.shields.io/npm/v/@mady9613/chess-engine)](https://www.npmjs.com/package/@mady9613/chess-engine)
[![npm downloads](https://img.shields.io/npm/dm/@mady9613/chess-engine)](https://www.npmjs.com/package/@mady9613/chess-engine)
[![GitHub stars](https://img.shields.io/github/stars/madhu9613/chess-engine)](https://github.com/madhu9613/chess-engine)
[![License](https://img.shields.io/npm/l/@mady9613/chess-engine)](https://github.com/madhu9613/chess-engine/blob/main/LICENSE)

**A complete chess engine with move validation, FEN support, and utilities**

[📦 npm](https://www.npmjs.com/package/@mady9613/chess-engine) • 
[🐙 GitHub](https://github.com/madhu9613/chess-engine) • 
[📚 Docs](https://github.com/madhu9613/chess-engine#readme) • 
[🐛 Issues](https://github.com/madhu9613/chess-engine/issues)

</div>

---# @mady9613/chess-engine

Comprehensive chess engine for move validation and game state management.

- **npm:** https://www.npmjs.com/package/@mady9613/chess-engine  
- **Author:** [mady9613](https://www.npmjs.com/~mady9613)

---

## Installation

```bash
npm install @mady9613/chess-engine
```

---

## Quick Start

```js
import { ChessGame } from '@mady9613/chess-engine';

const game = new ChessGame();

const move = game.move('e2e4');
console.log(move.success); // true
console.log(move.san);     // "e4"
console.log(game.getFEN()); // Current FEN
```

---

## Main Class: `ChessGame`

### Create game

```js
const game = new ChessGame();           // start position
const gameFromFen = new ChessGame(fen); // from FEN
```

### Common methods

- `move(move, promotionPiece?)`
- `undo()`, `redo()`, `canUndo()`, `canRedo()`
- `reset()`
- `loadFEN(fen)`, `getFEN()`
- `loadPGN(pgn)`, `getPGN()`
- `getBoard()`, `getPieceAt(square)`, `getTurn()`
- `getValidMoves(square)`, `getAllValidMoves()`
- `isValidMove(move)`
- `isCheck()`, `isCheckmate()`, `isStalemate()`, `isDraw()`, `isGameOver()`
- `isThreefoldRepetition()`, `isFiftyMoveRule()`, `isInsufficientMaterial()`
- `getWinner()`, `getResult()`
- `getMoveHistory()`, `getMoves()`, `getLastMove()`, `getMoveCount()`
- `goToMove(index)`, `goToStart()`, `goToEnd()`
- `toJSON()`, `toObject()`, `clone()`, `fromJSON(data)`

### Static utility

- `ChessGame.isValidFEN(fen)`

---

## Move Input Format

Supported move input styles:

- UCI-like string: `"e2e4"`, `"e7e8q"`
- Object format: `{ from: 'e2', to: 'e4' }`
- Object with promotion: `{ from: 'e7', to: 'e8', promotion: 'q' }`

Promotion pieces: `q`, `r`, `b`, `n`

---

## Move Result Shape

`game.move(...)` returns:

```js
{
  success: true,
  san: 'e4',
  piece: 'wp',
  capture: false,
  check: false,
  checkmate: false,
  stalemate: false,
  promotion: null
}
```

If invalid:

```js
{ success: false, error: 'Illegal move' }
```

---

## Named Exports

The package also exposes lower-level helpers from `src/index.js`.

### Validators
- `getValidMoves`
- `getAllLegalMoves`
- `isMoveLegal`
- `isMoveLegalBasic`
- `isMoveLegalQuick`

### Piece move generators
- `getPawnMoves`
- `getKnightMoves`
- `getBishopMoves`
- `getRookMoves`
- `getQueenMoves`
- `getKingMoves`

### Board / notation / FEN utilities
- `getInitialBoardPosition`
- `getEmptyBoard`
- `copyBoard`
- `algebraicToCoord`
- `coordToAlgebraic`
- `isValidCoord`
- `getPieceAt`
- `isSquareAttacked`
- `doesPieceAttackSquare`
- `getSAN`
- `getDetailedSAN`
- `parseSAN`
- `boardToFEN`
- `FENToBoard`
- `getStartingFEN`
- `isValidFEN`

### Core move helpers
- `executeMove`
- `isCaptureMove`
- `isPromotionMove`
- `getMoveSAN`

---

## Example: Validate & Play Loop

```js
import { ChessGame } from '@mady9613/chess-engine';

const game = new ChessGame();
const moves = ['e2e4', 'e7e5', 'g1f3', 'b8c6'];

for (const m of moves) {
  const result = game.move(m);
  if (!result.success) {
    console.log('Invalid:', result.error);
    break;
  }
  console.log(result.san, game.getFEN());
}
```

---

## License

MIT
