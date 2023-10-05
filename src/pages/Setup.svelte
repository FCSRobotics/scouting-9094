<script lang="ts">
  export let setCurrentPage;

  let scouter = null;
  let schedule_text = "";
</script>

<input type="number" bind:value={scouter} />
{#if scouter != null}
  <h1>Enter the schedule sent to you here:</h1>
  <input type="text" bind:value={schedule_text} />
{/if}

<button
  on:click={() => {
    setCurrentPage(1, { scouter, raw_schedule: JSON.parse(schedule_text) });
  }}>Click</button
>
