<script lang="ts">
  let board: (string | null)[] = Array(9).fill(null);
  let currentPlayer: 'X' | 'O' = 'X';

  function handleClick(index: number): void {
    if (winner || board[index]) return;

    board[index] = currentPlayer;
      currentPlayer = currentPlayer === 'X' ? 'O' : 'X';
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
