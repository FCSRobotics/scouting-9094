<script lang="ts">
    import QrCode from "svelte-qrcode";
    type TeamGameData = {
    high_cones_auto: number;
    mid_cones_auto: number;
    low_cones_auto: number;
    high_cubes_auto: number;
    mid_cubes_auto: number;
    low_cubes_auto: number;
    mobility_auto: boolean;
    balanced_auto: 1 | 0 | 2;
    high_cones: number;
    mid_cones: number;
    low_cones: number;
    high_cubes: number;
    mid_cubes: number;
    low_cubes: number;
    defense: boolean;
    balanced: 1 | 0 | 2;
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

    export let setCurrentPage;
    export let scouter;
    export let index;
    export let schedule: TeamGameData[];console.log(schedule[index])
</script>

<main>
<label for="high_cones_auto">High cones auto: </label>
<input type="number" bind:value={schedule[index].high_cones_auto} name="high_cones_auto" id="high_cones_auto">
<label for="mid_cones_auto">Mid cones auto: </label>
<input type="number" bind:value={schedule[index].mid_cones_auto} name="mid_cones_auto" id="mid_cones_auto">
<label for="low_cones_auto">Low cones auto: </label>
<input type="number" bind:value={schedule[index].low_cones_auto} name="low_cones_auto" id="low_cones_auto">
<label for="high_cubes_auto">High cubes auto: </label>
<input type="number" bind:value={schedule[index].high_cubes_auto} name="high_cubes_auto" id="high_cubes_auto">
<label for="mid_cubes_auto">Mid cubes auto: </label>
<input type="number" bind:value={schedule[index].mid_cubes_auto} name="mid_cubes_auto" id="mid_cubes_auto">
<label for="low_cubes_auto">Low cubes auto: </label>
<input type="number" bind:value={schedule[index].low_cubes_auto} name="low_cubes_auto" id="low_cubes_auto">
<label for="mobility_auto">Mobility auto: </label>
<input type="checkbox" bind:checked={schedule[index].mobility_auto} name="mobility_auto" id="mobility_auto">
<label for="balanced_auto">Balanced auto: </label>
<select name="balanced_auto" bind:value={schedule[index].balanced_auto} id="balanced_auto">
    <option value={1}>Yes</option>
    <option value={0}>Didn't try</option>
    <option value={2}>Failed</option>
  </select>
  <label for="high_cones_auto">High cones: </label>
<input type="number" bind:value={schedule[index].high_cones} name="high_cones" id="high_cones">
<label for="mid_cones">Mid cones: </label>
<input type="number" bind:value={schedule[index].mid_cones} name="mid_cones" id="mid_cones">
<label for="low_cones">Low cones: </label>
<input type="number" bind:value={schedule[index].low_cones} name="low_cones" id="low_cones">
<label for="high_cubes">High cubes: </label>
<input type="number" bind:value={schedule[index].high_cubes} name="high_cubes" id="high_cubes">
<label for="mid_cubes">Mid cubes: </label>
<input type="number" bind:value={schedule[index].mid_cubes} name="mid_cubes" id="mid_cubes">
<label for="low_cubes">Low cubes: </label>
<input type="number" bind:value={schedule[index].low_cubes} name="low_cubes" id="low_cubes">
<label for="balanced">Balanced: </label>
<select name="balanced" bind:value={schedule[index].balanced} id="balanced">
    <option value={1}>Yes</option>
    <option value={0}>Didn't try</option>
    <option value={2}>Failed</option>
  </select>
  <label for="parked">Parked: </label>
<input type="checkbox" bind:checked={schedule[index].parked} name="parked" id="parked">
<label for="failure">Catastrophic failure: </label>
<input type="checkbox" bind:checked={schedule[index].catastrophic_failure} name="failure" id="failure">
<label for="sabotage">Sabotage: </label>
<input type="checkbox" bind:checked={schedule[index].sabotage} name="sabotage" id="sabotage">
<label for="drive_grade">Drive grade out of ten: </label>
<input type="number" bind:value={schedule[index].drive_grade} name="drive_grade" id="drive_grade">
<label for="overall_grade">Overall grade out of ten: </label>
<input type="number" bind:value={schedule[index].overall_grade} name="overall_grade" id="overall_grade">
<label for="notes">Notes: </label>
<input type="text" bind:value={schedule[index].notes} maxlength="150" name="notes" id="notes">
</main>

<QrCode value={JSON.stringify(schedule[index])} />

<button on:click={() => {setCurrentPage(1, {scouter, schedule})}}>Go back</button>
<style>
    main {
        display: flex;
        flex-direction: column;
        text-align: left;
        justify-content: flex-start;
        align-items: flex-start;
    }
</style>