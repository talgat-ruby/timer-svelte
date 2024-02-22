<script lang="ts">
    import Counter from "./Counter.svelte";

    let _c: string[] = []

    let counters: string[] = []

    const handleAddCounter = () => {
        counters = [...counters, crypto.randomUUID()];
    }

    const handleDeleteCounter = (event: CustomEvent) => {
        counters = counters.filter((id) => id !== event.detail);
    }
</script>

<div>
    <button type="button" on:click={handleAddCounter}>
        Add counter
    </button>
    <ul>
        {#each counters as id, i (id)}
            <li>
                <span>{i}</span>
                <Counter id={id} on:delete={handleDeleteCounter}/>
            </li>
        {/each}
    </ul>
</div>
