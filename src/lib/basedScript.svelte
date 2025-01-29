<script lang="ts">
    import { onMount } from 'svelte';
  
    let randomPokemon: any = null;
  
    onMount(async () => {
      try {
        const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=151");
        const data = await response.json();
  
        if (data.results.length > 0) {
          // Select a random Pokémon
          randomPokemon = data.results[Math.floor(Math.random() * data.results.length)];
        }
      } catch (err) {
        console.error("Error fetching Pokémon:", err);
      }
    });
  </script>
  
  {#if randomPokemon}
    <div>
      <img 
        class="hidden-pokemon"
        src={`https://img.pokemondb.net/sprites/black-white/normal/${randomPokemon.name}.png`}
        alt={randomPokemon.name}
      />
      <h3>{randomPokemon.name}</h3>
    </div>
  {:else}
    <div>One moment please...</div>
  {/if}
  
  <style>
    .hidden-pokemon {
      filter: brightness(0.1) contrast(1.5);
    }
  </style>
  