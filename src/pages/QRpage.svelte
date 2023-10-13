<script lang="ts">
  import QrCode from "svelte-qrcode";
  import type { TeamGameData } from "../lib/types";
  export let content: TeamGameData[][];

  export let goBack;

  function getValues(game: TeamGameData): string[] {
    let temp = []
    temp[0] = game.high_cones_auto;
    temp[1] = game.mid_cones_auto;
    temp[2] = game.low_cones_auto;
    temp[3] = game.high_cubes_auto;
    temp[4] = game.mid_cubes_auto;
    temp[5] = game.low_cubes_auto;
    temp[6] = game.mobility_auto;
    temp[7] = game.balanced_auto
    temp[8] = game.high_cones;
    temp[9] = game.mid_cones;
    temp[10] = game.low_cones;
    temp[11] = game.high_cubes;
    temp[12] = game.mid_cubes;
    temp[13] = game.low_cubes;
    temp[14] = game.defense;
    temp[15] = game.balanced;
    temp[16] = game.parked;
    temp[17] = game.catastrophic_failure;
    temp[18] = game.sabotage;
    temp[19] = game.drive_grade;
    temp[20] = game.overall_grade;
    temp[21] = game.notes;
    temp[22] = game.team;
    temp[23] = game.match_number;
    temp[24] = game.done;
    temp[25] = game.won;
    return temp.map((value) => JSON.stringify(value));
  }
</script>

{#each content as code}
  <QrCode size="1000" value={JSON.stringify(code.map((game) => getValues(game)))} />
  <p>
    Matches: {code
      .map((it) => `${it.match_number}-${it.team.number}`)
      .join(", ")}
  </p>
  <p>{JSON.stringify(code.map((game) => getValues(game)))}</p>
{/each}
<button on:click={() => goBack()}>Back</button>

<style>
</style>
