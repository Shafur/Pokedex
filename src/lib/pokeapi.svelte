<script lang="ts">
import { error } from "@sveltejs/kit";
import { onMount } from 'svelte';
export let curl: Promise<any>;
export let pokemonName: string = ""; // Store Pokémon name
export const randomID = Math.floor(Math.random() * 151) + 1; // Random Pokémon ID

onMount(() => {
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
            src={`https://img.pokemondb.net/sprites/black-white/normal/${pokemon.name}.png`}
            alt={pokemon.name}
            />
            <h3>{pokemon.name}</h3>
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