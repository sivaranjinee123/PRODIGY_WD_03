# PRODIGY_WD_03
#Tic Toc Toe

<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Tic-Tac-Toe</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      background-color: #111;
      color: #fff;
      display: flex;
      flex-direction: column;
      align-items: center;
      padding-top: 50px;
    }

    h1 {
      margin-bottom: 20px;
    }

    .board {
      display: grid;
      grid-template-columns: repeat(3, 100px);
      grid-template-rows: repeat(3, 100px);
      gap: 5px;
    }

    .cell {
      width: 100px;
      height: 100px;
      font-size: 2rem;
      display: flex;
      justify-content: center;
      align-items: center;
      background-color: #222;
      cursor: pointer;
      transition: background-color 0.2s;
    }

    .cell:hover {
      background-color: #333;
    }

    .status {
      margin-top: 20px;
      font-size: 1.2rem;
    }

    button {
      margin-top: 20px;
      padding: 10px 20px;
      background-color: #0d6efd;
      border: none;
      color: white;
      border-radius: 5px;
      cursor: pointer;
    }

    button:hover {
      background-color: #0b5ed7;
    }
  </style>
</head>
<body>

  <h1>Tic-Tac-Toe</h1>
  <div class="board" id="board">
    <!-- 9 cells will be added here dynamically -->
  </div>
  <div class="status" id="status">Player X's turn</div>
  <button onclick="resetGame()">Reset Game</button>

  <script>
    const boardElement = document.getElementById('board');
    const statusElement = document.getElementById('status');

    let board = Array(9).fill('');
    let currentPlayer = 'X';
    let gameActive = true;

    const winningCombos = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ];

    function renderBoard() {
      boardElement.innerHTML = '';
      board.forEach((cell, index) => {
        const div = document.createElement('div');
        div.classList.add('cell');
        div.textContent = cell;
        div.addEventListener('click', () => handleClick(index));
        boardElement.appendChild(div);
      });
    }

    function handleClick(index) {
      if (!gameActive || board[index]) return;

      board[index] = currentPlayer;
      renderBoard();
      if (checkWinner()) {
        statusElement.textContent = `Player ${currentPlayer} wins!`;
        gameActive = false;
        return;
      }

      if (board.every(cell => cell !== '')) {
        statusElement.textContent = "It's a draw!";
        gameActive = false;
        return;
      }
	currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
      statusElement.textContent = `Player ${currentPlayer}'s turn`;
    }

    function checkWinner() {
      return winningCombos.some(combo => {
        const [a, b, c] = combo;
        return (
          board[a] &&
          board[a] === board[b] &&
          board[a] === board[c]
        );
      });
    }

    function resetGame() {
      board = Array(9).fill('');
      currentPlayer = 'X';
      gameActive = true;
      statusElement.textContent = `Player ${currentPlayer}'s turn`;
      renderBoard();
    }

    renderBoard();
  </script>
</body>
</html>
