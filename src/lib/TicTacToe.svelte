<script lang="ts">
  let board: (string | null)[] = Array(9).fill(null);
  let currentPlayer: 'X' | 'O' = 'X';
  let winner: string | null = null;
  let isDraw: boolean = false;

  function handleClick(index: number): void {
    if (winner || board[index]) return;

    board[index] = currentPlayer;
    if (checkWinner()) {
      winner = currentPlayer;
    } else if (board.every(cell => cell)) {
      isDraw = true;
    } else {
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
    }
  }

  function checkWinner(): boolean {
    const winningCombinations = [
      [0, 1, 2], [3, 4, 5], [6, 7, 8], // rows
      [0, 3, 6], [1, 4, 7], [2, 5, 8], // columns
      [0, 4, 8], [2, 4, 6]             // diagonals
    ];

    return winningCombinations.some(combination => {
      const [a, b, c] = combination;
      return board[a] && board[a] === board[b] && board[a] === board[c];
    });
  }

  function resetGame(): void {
    board = Array(9).fill(null);
    currentPlayer = 'X';
    winner = null;
    isDraw = false;
  }
</script>

<style>
  .board {
    display: grid;
    grid-template-columns: repeat(3, 100px);
    grid-gap: 5px;
    margin: 20px auto;
  }
  .cell {
    width: 100px;
    height: 100px;
    display: flex;
    justify-content: center;
    align-items: center;
    font-size: 2rem;
    background-color: #eee;
    color: black;
    cursor: pointer;
  }
  .winner {
    margin-top: 20px;
    text-align: center;
  }
  button {
    margin-top: 10px;
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
</style>

<div class="board">
  {#each board as cell, index}
    <div class="cell" on:click={() => handleClick(index)}>
      {cell === null ? "" : cell}
    </div>
  {/each}
</div>

{#if winner}
  <div class="winner">Player {winner} wins!</div>
{:else if isDraw}
  <div class="winner">It's a draw!</div>
{/if}

<button on:click={resetGame}>Reset Game</button>
