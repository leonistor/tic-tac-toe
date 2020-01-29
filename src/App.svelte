<script>
  import "./tailwind.css";
  import "animate.css";

  import { GithubIcon } from "svelte-feather-icons";
  import Button from "./Button.svelte";

  const initialBoard = Array(9).fill(" ");
  let board = Array.from(initialBoard); // hah!
  let nextPlayer = "X";
  let winningCombination;
  let winningPlayer;
  const rows = [[0, 1, 2], [3, 4, 5], [6, 7, 8]];
  const possibleWinningCombinations = [
    // rows
    [0, 1, 2],
    [3, 4, 5],
    [6, 7, 8],
    // columns
    [0, 3, 6],
    [1, 4, 7],
    [2, 5, 8],
    // diagonals
    [0, 4, 8],
    [6, 4, 2]
  ];

  function checkWinningCondition() {
    return possibleWinningCombinations
      .filter(combination => {
        return (
          board[combination[0]] != " " &&
          board[combination[0]] === board[combination[1]] &&
          board[combination[1]] === board[combination[2]]
        );
      })
      .pop(); // winning combination or undefined
  }

  function getWinningPlayer() {
    return board[winningCombination[0]];
  }

  function getWinner() {
    winningCombination = checkWinningCondition();
    if (winningCombination) {
      winningPlayer = getWinningPlayer();
    }
    if (!board.includes(" ") && !winningPlayer) {
      // no more moves
      winningPlayer = "TIE";
    }
  }

  function handleClick(i) {
    if (board[i] != " " || winningCombination) {
      flash();
    } else {
      board[i] = nextPlayer;
      nextPlayer = nextPlayer === "X" ? "O" : "X";
      // console.log(winningCombination);
      getWinner();
    }
  }

  function clearState() {
    board = [...initialBoard];
    nextPlayer = "X";
    winningCombination = null;
    winningPlayer = null;
  }

  let blink = "";

  function flash() {
    blink = "animated shake fast";
    setTimeout(() => {
      blink = "";
    }, 800);
  }
</script>

<style>

</style>

<main class="max-w-lg min-h-screen mx-auto bg-white">
  <div class="flex flex-col items-center justify-center h-screen p-6">

    <h1 class="text-4xl font-thin text-gray-600">Tic-Tac-Toe</h1>

    {#if winningPlayer}
      <h3 class="text-2xl text-red-700 animated slideInUp">
        Winner:
        <span class="text-blue font-bold">{winningPlayer}</span>
      </h3>
    {:else}
      <h3 class="text-2xl text-gray-700">
        Next player:
        <span class="text-blue-900 text-center inline-block w-6">
          {nextPlayer.toUpperCase()}
        </span>
      </h3>
    {/if}

    <div class="{blink} mt-2">
      {#each rows as row}
        <div>
          {#each row as index}
            <Button
              clickHandler={() => handleClick(index)}
              value={board[index]}
              highlight={!!winningCombination && winningCombination.includes(index)} />
          {/each}
        </div>
      {/each}
    </div>

    <button
      on:click={clearState}
      class="py-1 px-2 mt-6 rounded bg-gray-600 text-white focus:outline-none">
      Reset
    </button>
  </div>
  <footer class="absolute bottom-0 left-0 py-2 w-full">
    <div class="text-center mx-auto text-sm text-gray-600">
      <a href="https://github.com/leonistor/tic-tac-toe" target="_blank">
        <span class="inline-block items-baseline">
          <GithubIcon size="12" />
        </span>
        leonistor/tic-tac-toe
      </a>
    </div>

  </footer>
</main>
