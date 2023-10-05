<script lang="ts">
  export let setCurrentPage;
  export let scouter: number;
  export let schedule = [] as TeamGameData[] | null;
  console.log(schedule[0])

  type TeamGameData = {
    high_cones_auto: number;
    mid_cones_auto: number;
    low_cones_auto: number;
    high_cubes_auto: number;
    mid_cubes_auto: number;
    low_cubes_auto: number;
    mobility_auto: boolean;
    balanced_auto: 'yes' | 'no' | 'failed';
    high_cones: number;
    mid_cones: number;
    low_cones: number;
    high_cubes: number;
    mid_cubes: number;
    low_cubes: number;
    defense: boolean;
    balanced: 'yes' | 'no' | 'failed';
    parked: boolean;
    catastrophic_failure: boolean;
    sabotage: boolean;
    drive_grade: number;
    overall_grade: number;
    notes: string;
    team: Team;
    match: number;
  };
  type Team = {
	  name: string | null;
	  number: string;
  };

</script>

<main>
{#each schedule as match, i}
  <button class="list-item" on:click={() => {setCurrentPage(2, {index: i, schedule, scouter, setCurrentPage})}}><p>Match: {match.match}</p><p>{match.team.number}</p></button>
{/each}
</main>

<style>
  main {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
  }
  .list-item {
    width: 100%;
  }
</style>