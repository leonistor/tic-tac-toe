<script>
  export let value = " ";
  export let highlight = false;
  export let clickHandler = null;
</script>

<button
  on:click={clickHandler}
  class:bg-blue-700={highlight}
  class="w-16 h-16 m-2 focus:outline-none rounded text-center font-bold
  align-middle bg-blue-400 text-white text-3xl">
  {value}
</button>
