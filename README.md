<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <title>AIオセロ</title>
    <link rel="stylesheet" href="style.css">
  </head>
  <body>
    <h1>AIオセロ</h1>
    <table>
      <tbody>
        <tr>
          <td class="square" data-row="0" data-col="0"></td>
          <td class="square" data-row="0" data-col="1"></td>
          <td class="square" data-row="0" data-col="2"></td>
          <td class="square" data-row="0" data-col="3"></td>
          <td class="square" data-row="0" data-col="4"></td>
          <td class="square" data-row="0" data-col="5"></td>
          <td class="square" data-row="0" data-col="6"></td>
          <td class="square" data-row="0" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="1" data-col="0"></td>
          <td class="square" data-row="1" data-col="1"></td>
          <td class="square" data-row="1" data-col="2"></td>
          <td class="square" data-row="1" data-col="3"></td>
          <td class="square" data-row="1" data-col="4"></td>
          <td class="square" data-row="1" data-col="5"></td>
          <td class="square" data-row="1" data-col="6"></td>
          <td class="square" data-row="1" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="2" data-col="0"></td>
          <td class="square" data-row="2" data-col="1"></td>
          <td class="square" data-row="2" data-col="2"></td>
          <td class="square" data-row="2" data-col="3"></td>
          <td class="square" data-row="2" data-col="4"></td>
          <td class="square" data-row="2" data-col="5"></td>
          <td class="square" data-row="2" data-col="6"></td>
          <td class="square" data-row="2" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="3" data-col="0"></td>
          <td class="square" data-row="3" data-col="1"></td>
          <td class="square" data-row="3" data-col="2"></td>
          <td class="square" data-row="3" data-col="3"></td>
          <td class="square" data-row="3" data-col="4"></td>
          <td class="square" data-row="3" data-col="5"></td>
          <td class="square" data-row="3" data-col="6"></td>
          <td class="square" data-row="3" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="4" data-col="0"></td>
          <td class="square" data-row="4" data-col="1"></td>
          <td class="square" data-row="4" data-col="2"></td>
          <td class="square" data-row="4" data-col="3"></td>
          <td class="square" data-row="4" data-col="4"></td>
          <td class="square" data-row="4" data-col="5"></td>
          <td class="square" data-row="4" data-col="6"></td>
          <td class="square" data-row="4" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="5" data-col="0"></td>
          <td class="square" data-row="5" data-col="1"></td>
          <td class="square" data-row="5" data-col="2"></td>
          <td class="square" data-row="5" data-col="3"></td>
          <td class="square" data-row="5" data-col="4"></td>
          <td class="square" data-row="5" data-col="5"></td>
          <td class="square" data-row="5" data-col="6"></td>
          <td class="square" data-row="5" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="6" data-col="0"></td>
          <td class="square" data-row="6" data-col="1"></td>
          <td class="square" data-row="6" data-col="2"></td>
          <td class="square" data-row="6" data-col="3"></td>
          <td class="square" data-row="6" data-col="4"></td>
          <td class="square" data-row="6" data-col="5"></td>
          <td class="square" data-row="6" data-col="6"></td>
          <td class="square" data-row="6" data-col="7"></td>
        </tr>
        <tr>
          <td class="square" data-row="7" data-col="0"></td>
          <td class="square" data-row="7" data-col="1"></td>
          <td class="square" data-row="7" data-col="2"></td>
          <td class="square" data-row="7" data-col="3"></td>
          <td class="square" data-row="7" data-col="4"></td>
          <td class="square" data-row="7" data-col="5"></td>
          <td class="square" data-row="7" data-col="6"></td>
          <td class="square" data-row="7" data-col="7"></td>
        </tr>
       </tbody>
       </table>


const player1 = "black"; // プレイヤー1の色
const player2 = "white"; // プレイヤー2の色
let currentPlayer = player1; // 現在のプレイヤーを初期化
const board = []; // 盤面を表す2次元配列
const squares = document.querySelectorAll(".square"); // 盤面のマスを取得


<script>
// 盤面を初期化する関数
function initializeBoard() {
  for (let i = 0; i < 8; i++) {
    board[i] = [];
    for (let j = 0; j < 8; j++) {
      board[i][j] = null;
    }
  }
  board[3][3] = player1;
  board[3][4] = player2;
  board[4][3] = player2;
  board[4][4] = player1;
}

// 盤面を描画する関数
function drawBoard() {
  for (let i = 0; i < squares.length; i++) {
    const row = squares[i].getAttribute("data-row");
    const col = squares[i].getAttribute("data-col");
    squares[i].classList.remove(player1, player2);
    if (board[row][col]) {
      squares[i].classList.add(board[row][col]);
    }
  }
}

// マスがクリックされた時に呼ばれる関数
function handleClick() {
  const row = this.getAttribute("data-row");
  const col = this.getAttribute("data-col");
  if (isValidMove(row, col)) {
    board[row][col] = currentPlayer;
    flipPieces(row, col);
    if (currentPlayer === player1) {
      currentPlayer = player2;
    } else {
      currentPlayer = player1;
    }
    drawBoard();
    updateScore();
    checkEndGame();
  }
}

// 石を裏返す関数
function flipPieces(row, col) {
  const directions = ["up", "down", "left", "right", "upleft", "upright", "downleft", "downright"];
  for (let i = 0; i < directions.length; i++) {
    const flippedPieces = getFlippedPieces(row, col, directions[i]);
    for (let j = 0; j < flippedPieces.length; j++) {
      const flippedRow = flippedPieces[j][0];
      const flippedCol = flippedPieces[j][1];
      board[flippedRow][flippedCol] = currentPlayer;
    }
  }
}

// 指定された方向にある裏返すべき石を取得する関数
function getFlippedPieces(row, col, direction) {
  const flippedPieces = [];
  let currentRow = parseInt(row);
  let currentCol = parseInt(col);
  let nextRow = currentRow + getRowOffset(direction);
  let nextCol = currentCol + getColOffset(direction);
  while (isValidPosition(nextRow, nextCol) && board[nextRow][nextCol] && board[nextRow][nextCol] !== currentPlayer) {
    flippedPieces.push([nextRow, nextCol]);
    currentRow = nextRow;
    currentCol = nextCol;
    nextRow = currentRow + getRowOffset(direction);
    nextCol = currentCol + getColOffset(direction);
  }
  if (isValidPosition(nextRow, nextCol) && board[nextRow][nextCol] === currentPlayer) {
    return flipped

} else {
return [];
}
}

// 指定された方向に対して、行方向のオフセットを取得する関数
function getRowOffset(direction) {
if (direction.indexOf("up") !== -1) {
return -1;
} else if (direction.indexOf("down") !== -1) {
return 1;
} else {
return 0;
}
}

// 指定された方向に対して、列方向のオフセットを取得する関数
function getColOffset(direction) {
if (direction.indexOf("left") !== -1) {
return -1;
} else if (direction.indexOf("right") !== -1) {
return 1;
} else {
return 0;
}
}

// 指定されたマスが有効な着手かどうかを判定する関数
function isValidMove(row, col) {
if (board[row][col]) {
return false;
}
const directions = ["up", "down", "left", "right", "upleft", "upright", "downleft", "downright"];
for (let i = 0; i < directions.length; i++) {
if (hasOpponentPiece(row, col, directions[i])) {
return true;
}
}
return false;
}

// 指定されたマスが有効な位置かどうかを判定する関数
function isValidPosition(row, col) {
return row >= 0 && row < 8 && col >= 0 && col < 8;
}

// 指定されたマスから指定された方向に対して、相手の石があるかどうかを判定する関数
function hasOpponentPiece(row, col, direction) {
const opponent = currentPlayer === player1 ? player2 : player1;
let currentRow = parseInt(row);
let currentCol = parseInt(col);
let nextRow = currentRow + getRowOffset(direction);
let nextCol = currentCol + getColOffset(direction);
while (isValidPosition(nextRow, nextCol) && board[nextRow][nextCol] === opponent) {
currentRow = nextRow;
currentCol = nextCol;
nextRow = currentRow + getRowOffset(direction);
nextCol = currentCol + getColOffset(direction);
}
if (isValidPosition(nextRow, nextCol) && board[nextRow][nextCol] === currentPlayer) {
return true;
} else {
return false;
}
}

// スコアを更新する関数
function updateScore() {
let blackCount = 0;
let whiteCount = 0;
for (let i = 0; i < 8; i++) {
for (let j = 0; j < 8; j++) {
if (board[i][j] === player1) {
blackCount++;
} else if (board[i][j] === player2) {
whiteCount++;
}
}
}
const blackScore = document.getElementById("black-score");
const whiteScore = document.getElementById("white-score");
blackScore.textContent = blackCount;
whiteScore.textContent = whiteCount;
}

// ゲームが終了したかどうかをチェックする関数
function checkEndGame() {
if (isBoardFull() || !has

validMove()) {
currentPlayer = currentPlayer === player1 ? player2 : player1;
updateScore();
displayBoard();
checkPossibleMoves();
if (!hasValidMove()) {
currentPlayer = currentPlayer === player1 ? player2 : player1;
checkPossibleMoves();
if (!hasValidMove()) {
endGame();
}
}
}
}

// ゲームが終了したことを表示する関数
function endGame() {
const message = document.getElementById("message");
const winner = getWinner();
if (winner) {
message.textContent = ${winner} wins!;
} else {
message.textContent = "Tie game!";
}
}

// 勝者を取得する関数
function getWinner() {
const blackCount = parseInt(document.getElementById("black-score").textContent);
const whiteCount = parseInt(document.getElementById("white-score").textContent);
if (blackCount > whiteCount) {
return "Black";
} else if (whiteCount > blackCount) {
return "White";
} else {
return null;
}
}

// オセロボードを初期化する関数
function initBoard() {
board = [];
for (let i = 0; i < 8; i++) {
board.push([]);
for (let j = 0; j < 8; j++) {
board[i][j] = null;
}
}
board[3][3] = player1;
board[3][4] = player2;
board[4][3] = player2;
board[4][4] = player1;
}

// ゲームを開始する関数
function startGame() {
initBoard();
updateScore();
displayBoard();
checkPossibleMoves();
}

// ゲームを再開する関数
function restartGame() {
currentPlayer = player1;
initBoard();
updateScore();
displayBoard();
checkPossibleMoves();
}

// ゲームをリセットする関数
function resetGame() {
const message = document.getElementById("message");
message.textContent = "";
restartGame();
}

// ゲームを初期化する関数
function initGame() {
const startButton = document.getElementById("start-button");
const resetButton = document.getElementById("reset-button");
const restartButton = document.getElementById("restart-button");
startButton.addEventListener("click", startGame);
resetButton.addEventListener("click", resetGame);
restartButton.addEventListener("click", restartGame);
}

initGame();

</script>
</body>
</html>
