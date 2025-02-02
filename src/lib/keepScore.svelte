<script lang="ts">
    import { updated } from "$app/state";
    import Pokeapi from "./pokeapi.svelte";

    let count =$state(0);
    let src = "https://media.tenor.com/0ag0MVXUaQEAAAAM/team-rocket-blasting-off-again.gif";
    let userInput = $state("");

    function increment() {
        count += 1;
    }

    function handleKeyDown(event) {
    if (event.key === "Enter") {
      userInput = ""; // Optional: Clears the input field
    }
  }

</script>

<input bind:value={userInput} onkeydown={handleKeyDown}/>
<h2></h2>




<button onclick={increment}>
    Correct: {count}
</button>

{#if count < 5}
    <p>Dawg, c'mon...</p>
{:else if count < 10 && count >=5}
    <p> Hol' updated, let him cook.</p>
{:else if count >= 10}
    <p>SIGMA POKEMON RUZZ!!! WE'RE BLASTING OFF AGAIN!?!?</p>
    <img {src} alt="Team Rocket" />
{/if}