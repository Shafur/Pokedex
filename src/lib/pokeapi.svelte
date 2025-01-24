<script lang="ts">
   import { onMount } from 'svelte';
   let curl: Promise<any>;
    onMount(async () => {
        
        const response = await fetch("https://pokeapi.co/api/v2/pokemon?limit=151/");
        curl = response.json();

    });
</script>

{#await curl}
 <div>One moment please...</div>
{:then results}
 <pre>{JSON.stringify(results, null, 2)}</pre>
{:catch error}
<div>{error.message}</div>
{/await}