<script lang="ts">
    let elapsed = $state(30);
    let interval = $state(1000);

    $effect(() => {
    setInterval(() => {
        elapsed += -1;
    }, interval);
});
</script>



{#if elapsed > 0}
    <p>elapsed time: {elapsed}</p>
{:else if elapsed <= 0}
    <p>TIMES UP, PENCILS DOWN!</p>
{/if}