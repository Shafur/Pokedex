<script lang="ts">
import { error } from "@sveltejs/kit";
import { onMount } from 'svelte';
   let curl: Promise<any>;
    onMount(() => {
        
         curl = fetch("https://pokeapi.co/api/v2/pokemon?limit=151").then((pokedata) => pokedata.json());
    });


</script>

{#await curl}

    <div>One moment please...</div>

{:then results}

    {#each results?.results ?? [] as pokemon}
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