<script lang="ts">
import { error } from "@sveltejs/kit";
import { onMount } from 'svelte';
 let curl = $state();
 let {pokemonName = $bindable(), randomID = $bindable()} = $props(); 


$effect(() => {
    console.log(pokemonName);
    curl = fetch(`https://pokeapi.co/api/v2/pokemon/${randomID}`)
        .then((pokedata) => pokedata.json())
        .then((results) => {
            if (results.forms && results.forms.length > 0) {
                pokemonName = results.forms[0].name; // Store first form's name
                console.log("Fetched Pokémon name:", pokemonName); // Debugging
            } else {
                console.error("No forms found for this Pokémon.");
            }
            return results;
        })
        .catch((err) => {
            console.error("Error fetching Pokémon:", err);
        });

});
</script>

{#await curl}

    <div>One moment please...</div>

{:then results}

    {#each results?.forms ?? [] as pokemon}
       <div> 
            <img 
            class="hidden-pokemon"
            src={`https://img.pokemondb.net/sprites/black-white/anim/normal/${pokemon.name}.gif`}
            alt={pokemon.name}
            />
            <h3></h3>
        </div>
     {/each}

{:catch error}

    <div>{error.message}</div>

{/await}



<style>
    
    .hidden-pokemon{
        filter: brightness(0.1) contrast(1.5);
    }
</style>