<script lang="ts">
    import { updated } from "$app/state";
    import Pokeapi from "./pokeapi.svelte";
    import { fade } from "svelte/transition";

    let count =$state(0);
    let correctStreak = $state(0);
    let src = "https://media.tenor.com/0ag0MVXUaQEAAAAM/team-rocket-blasting-off-again.gif";
    let userInput = $state("");
    let pokeName = $state("");
    let incorrectName = $state("");
    let correctName = $state("");
    let randomID = $state(Math.floor(Math.random() * 151) + 1);
    
    let opacity = 1;


    function handleKeyDown(event) {
    if (event.key === "Enter") {
        console.log("userinput:", userInput);
        console.log("pokemonname:", pokeName)

        if (!pokeName) {
            pokeName;
            console.log("nope.");
            return;
        }
        if (userInput.toLowerCase() === pokeName.toLowerCase()) {
            
            count += 1;
            correctName = pokeName;
            setTimeout(() => {
                correctName = "";
            }, 3000);
            
        } else {
            incorrectName = pokeName;
            count = 0;

            setTimeout(() => {
                incorrectName = "";
            }, 3000);
        }
        userInput = "";
        randomID = Math.floor(Math.random() * 151) + 1;
        if (count > correctStreak) {
            correctStreak = count;
        }
    }
       // Optional: Clears the input field
    }

    
  


</script>
<Pokeapi bind:pokemonName={pokeName} bind:randomID/>
<input type ="text" bind:value={userInput} onkeydown={handleKeyDown}/>


<div>
    Correct: {count}
    High Score: {correctStreak}
</div>



{#if correctStreak < 5}
    <p>Dawg, c'mon...</p>
{:else if correctStreak < 10 && correctStreak >=5}
    <p> Hol' updated, let him cook.</p>
{:else if correctStreak >= 10}
    <p>SIGMA POKEMON RUZZ!!! WE'RE BLASTING OFF AGAIN!?!?</p>
    <img {src} alt="Team Rocket" />
{/if}


{#if incorrectName}
<h2 style="color: red;" transition:fade>{incorrectName}</h2>
{/if}
{#if correctName}
<h2 style="color: green;" transition:fade>{correctName}</h2>
{/if}

<style>
    wrongAnswer {
        color: red;
        opacity: 1;
        transition: opacity 3s ease;
    }
 
</style>