<script lang="ts">
  import QrCode from "svelte-qrcode";
  import type { TeamGameData } from "../lib/types";
  export let content: TeamGameData[][];

  export let goBack;
</script>

{#each content as code}
  <QrCode size="1000" value={JSON.stringify(code)} />
  <p>
    Matches: {code
      .map((it) => `${it.match_number}-${it.team.number}`)
      .join(", ")}
  </p>
{/each}
<button on:click={() => goBack()}>Back</button>

<style>
</style>
