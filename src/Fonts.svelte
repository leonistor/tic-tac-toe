<script>
  let weights = [
    "font-hairline",
    "font-thin",
    "font-light",
    "font-normal",
    "font-medium",
    "font-semibold",
    "font-bold",
    "font-extrabold",
    "font-black"
  ];

  function titleCase(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  }
</script>

{#each weights as weight}
  <div class="mt-4">
    <span class="bg-gray-800 text-white rounded px-2 py-1">
      {weight.substring(5)}
    </span>
    <p class="{weight} text-4xl">Montserrat {titleCase(weight.substring(5))}</p>
    <p class="{weight} italic text-4xl">
      Montserrat {titleCase(weight.substring(5))} Italic
    </p>
  </div>
{/each}
