<script lang="ts">
    import { updated } from "$app/state";
    import Pokeapi from "./pokeapi.svelte";

    let count =$state(0);
    let src = "https://media.tenor.com/0ag0MVXUaQEAAAAM/team-rocket-blasting-off-again.gif";
    let userInput = $state("");
    let pokeName = "";
    let randomID = Math.floor(Math.random() * 151) + 1;



    function handleKeyDown(event) {
    if (event.key === "Enter") {
        console.log("userinput:", userInput);
        console.log("pokemonname:", pokeName)

        if (!pokeName) {
            console.log("nope.");
            return;
        }
        if (userInput.toLowerCase() === pokeName.toLowerCase()) {
            count += 1;
            randomID = Math.floor(Math.random() * 151) + 1;
        }
        userInput = "";
    }
       // Optional: Clears the input field
    }
  


</script>
<Pokeapi bind:pokemonName={pokeName} bind:randomID={randomID}/>
<input type ="text" bind:value={userInput} onkeydown={handleKeyDown}/>
<h2></h2>




<button>
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