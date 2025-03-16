<script lang="ts">
import Pokeapi from "../lib/pokeapi.svelte";
import Based from "../lib/basedScript.svelte";
import TimeComp from "../lib/timeComp.svelte";
import KeepScore from "$lib/keepScore.svelte";

let startGame = false;
</script>

<div class = "button-container">
    <button
        class="bg-white border shadow-sm px-12 roundedmd py-2"
        on:click={() => {startGame = !startGame}}
        >{startGame ? "End Game" : "Start Game: Click to Begin!"}
    </button>

    {#if startGame}
    <div class="center-container">
        <TimeComp />
        <KeepScore />
    </div>
    {/if}
</div>

<style>
    .button-container {
        display: flex;
        justify-content: center;
        margin-top: 20px;
    }

    .center-container {
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        position: absolute;
        top: 25%;
        left: 50%;
        transform: translate(-50%, 50%);
        text-align: center;
    }
</style>





