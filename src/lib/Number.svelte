<script>
    export let value = 0;
    export let id;
</script>
<div class="containerguy">


<button on:click={() => value--}>-</button>
<input type="number" min="0" bind:value={value} name={id} {id}>
<button on:click={() => value++}>+</button>
</div>

<style>
    .containerguy {
        display: flex;
        align-items: flex-start;
        justify-content: flex-start;
        width:100%;
        height: 100%;
        flex-direction: row;
    }

    input {
        width: 3vw;
    }
</style>