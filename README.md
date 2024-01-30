<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Tic Tac Toe Game </title>
  <style>
    body {
      font-family: 'Arial', sans-serif;
      text-align: center;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      gap: 5px;
      margin: 20px auto;
    }
    .cell {
      width: 100px;
      height: 100px;
      border: 5px solid #021839;
      font-size: 4em;
      cursor: pointer;
    }
  </style>
</head>
<body>

  <h1>💕💕💕💕Tic Tac Toe💕💕💕💕</h1>
 
  <div id="message"></div>

  <div class="board" id="board">
    <div class="cell" data-index="0"></div>
    <div class="cell" data-index="1"></div>
    <div class="cell" data-index="2"></div>
    <div class="cell" data-index="3"></div>
    <div class="cell" data-index="4"></div>
    <div class="cell" data-index="5"></div>
    <div class="cell" data-index="6"></div>
    <div class="cell" data-index="7"></div>
    <div class="cell" data-index="8"></div>
  </div>

  <script>
    document.addEventListener('DOMContentLoaded', function () {
      const board = document.getElementById('board');
      const cells = document.querySelectorAll('.cell');
      const message = document.getElementById('message');
      let currentPlayer = 'X';
      let gameBoard = ['', '', '', '', '', '', '', '', ''];
      let gameActive = true;

      function checkWinner() {
        const winPatterns = [
          [0, 1, 2],
          [3, 4, 5],
          [6, 7, 8],
          [0, 3, 6],
          [1, 4, 7],
          [2, 5, 8],
          [0, 4, 8],
          [2, 4, 6]
        ];

        for (let pattern of winPatterns) {
          const [a, b, c] = pattern;
          if (gameBoard[a] && gameBoard[a] === gameBoard[b] && gameBoard[a] === gameBoard[c]) {
            return gameBoard[a];
          }
        }

        return null;
      }

      function checkDraw() {
        return !gameBoard.includes('');
      }

      function handleClick(index) {
        if (!gameBoard[index] && gameActive) {
          gameBoard[index] = currentPlayer;
          cells[index].textContent = currentPlayer;

          const winner = checkWinner();
          if (winner) {
            message.textContent = `${winner} 👈👈❤️congratulation❤️`;
            gameActive = false;
          } else if (checkDraw()) {
            message.textContent = 'It\'s a draw!';
            gameActive = false;
          } else {
            currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
            message.textContent = `Current Player: ${currentPlayer}`;
          }
        }
      }

      cells.forEach((cell, index) => {
        cell.addEventListener('click', () => handleClick(index));
      });
    });
  </script>

</body>
</html>
