<script lang="ts">
  export let setCurrentPage;

  let scouter = null;
  let schedule_text = "";

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
    done: boolean;
  };
  type Team = {
	  name: string | null;
	  number: string;
  };

  function parseSchedule(raw: string, scout: number): TeamGameData[] {
    let data = [] as TeamGameData[];
    if (raw.schedule == undefined || raw.schedule == null) return [];
    raw.schedule.forEach((match) => {

      data.push(
        ...Object.keys(match.team_assignments)
          .filter((it) => match.team_assignments[it] == scout)
          .map((it) => ({ team: {number:it as string}, match: match.match_number as number, won: false, cubes: 0, cones: 0 }))
      );
    });
    data.sort((a, b) => a.match > b.match ? 1 : -1)
    console.log(data)
    return data;
  }
</script>

<input type="number" bind:value={scouter} />
{#if scouter != null}
  <h1>Enter the schedule sent to you here:</h1>
  <input type="text" bind:value={schedule_text} />
{/if}

<button
  on:click={() => {
    setCurrentPage(1, { scouter, schedule: parseSchedule(JSON.parse(schedule_text), scouter) });
  }}>Click</button
>
