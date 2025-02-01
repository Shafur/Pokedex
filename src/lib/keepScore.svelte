<script lang="ts">
    import { updated } from "$app/state";

    let count =$state(0);
    let src = "https://media.tenor.com/0ag0MVXUaQEAAAAM/team-rocket-blasting-off-again.gif";

    function increment() {
        count += 1;
    }
</script>

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