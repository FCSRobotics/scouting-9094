<script lang="ts">
	import QrCode from "svelte-qrcode";
	import Number from "../lib/Number.svelte";
	import type { TeamGameData } from "../lib/types";

	export let setCurrentPage;
	export let scouter;
	export let index;
	export let schedule: TeamGameData[];
	$: (() => {
		localStorage.setItem("schedule", JSON.stringify(schedule));
		localStorage.setItem("scouter", scouter.toString());

		if (schedule[index].exported) schedule[index].exported = false;
	})();
	console.log(schedule[index]);
</script>

<h1>
	Team: {schedule[index].team.number} | Match: {schedule[index].match_number}
</h1>
<h2>Scouter number: {scouter + 1}</h2>
<main>
	<div class="column">
		<h3>Auto</h3>
		<label for="high_cones_auto">High cones auto: </label>
		<Number
			bind:value={schedule[index].high_cones_auto}
			name="high_cones_auto"
			id="high_cones_auto"
		/>
		<label for="mid_cones_auto">Mid cones auto: </label>
		<Number
			type="number"
			bind:value={schedule[index].mid_cones_auto}
			name="mid_cones_auto"
			id="mid_cones_auto"
		/>
		<label for="low_cones_auto">Low cones auto: </label>
		<Number
			type="number"
			bind:value={schedule[index].low_cones_auto}
			name="low_cones_auto"
			id="low_cones_auto"
		/>
		<label for="high_cubes_auto">High cubes auto: </label>
		<Number
			type="number"
			bind:value={schedule[index].high_cubes_auto}
			name="high_cubes_auto"
			id="high_cubes_auto"
		/>
		<label for="mid_cubes_auto">Mid cubes auto: </label>
		<Number
			type="number"
			bind:value={schedule[index].mid_cubes_auto}
			name="mid_cubes_auto"
			id="mid_cubes_auto"
		/>
		<label for="low_cubes_auto">Low cubes auto: </label>
		<Number
			type="number"
			bind:value={schedule[index].low_cubes_auto}
			name="low_cubes_auto"
			id="low_cubes_auto"
		/>
		<label for="mobility_auto">Mobility auto: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].mobility_auto}
			name="mobility_auto"
			id="mobility_auto"
		/>
		<label for="balanced_auto">Balanced auto: </label>
		<select
			name="balanced_auto"
			bind:value={schedule[index].balanced_auto}
			id="balanced_auto"
		>
			<option value={1}>Yes</option>
			<option value={0}>Didn't try</option>
			<option value={2}>Failed</option>
		</select>
	</div>
	<div class="column">
		<h3>Teleop</h3>
		<label for="high_cones">High cones: </label>
		<Number
			type="number"
			bind:value={schedule[index].high_cones}
			name="high_cones"
			id="high_cones"
		/>
		<label for="mid_cones">Mid cones: </label>
		<Number
			type="number"
			bind:value={schedule[index].mid_cones}
			name="mid_cones"
			id="mid_cones"
		/>
		<label for="low_cones">Low cones: </label>
		<Number
			type="number"
			bind:value={schedule[index].low_cones}
			name="low_cones"
			id="low_cones"
		/>
		<label for="high_cubes">High cubes: </label>
		<Number
			type="number"
			bind:value={schedule[index].high_cubes}
			name="high_cubes"
			id="high_cubes"
		/>
		<label for="mid_cubes">Mid cubes: </label>
		<Number
			type="number"
			bind:value={schedule[index].mid_cubes}
			name="mid_cubes"
			id="mid_cubes"
		/>
		<label for="low_cubes">Low cubes: </label>
		<Number
			type="number"
			bind:value={schedule[index].low_cubes}
			name="low_cubes"
			id="low_cubes"
		/>
		<label for="defense">Defense: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].defense}
			name="defense"
			id="defense"
		/>
		<label for="balanced">Balanced: </label>
		<select name="balanced" bind:value={schedule[index].balanced} id="balanced">
			<option value={1}>Yes</option>
			<option value={0}>Didn't try</option>
			<option value={2}>Failed</option>
		</select>
		<label for="parked">Parked: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].parked}
			name="parked"
			id="parked"
		/>
	</div>
	<div class="column">
		<h3>General</h3>
		<label for="failure">Catastrophic failure: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].catastrophic_failure}
			name="failure"
			id="failure"
		/>
		<label for="sabotage">Sabotage: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].sabotage}
			name="sabotage"
			id="sabotage"
		/>
		<label for="drive_grade">Drive grade out of ten: </label>
		<input
			type="number"
			bind:value={schedule[index].drive_grade}
			name="drive_grade"
			id="drive_grade"
		/>
		<label for="overall_grade">Overall grade out of ten: </label>
		<input
			type="number"
			bind:value={schedule[index].overall_grade}
			name="overall_grade"
			id="overall_grade"
		/>
		<label for="notes">Notes: </label>
		<textarea
			bind:value={schedule[index].notes}
			maxlength="150"
			name="notes"
			id="notes"
		/>
		<label for="won">Won: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].won}
			name="won"
			id="won"
		/>
		<label for="done">Mark as done: </label>
		<input
			type="checkbox"
			bind:checked={schedule[index].done}
			name="done"
			id="done"
		/>
	</div>
</main>

<QrCode value={JSON.stringify(schedule[index])} />
<p>{JSON.stringify(schedule[index])}</p>

<button
	on:click={() => {
		setCurrentPage(1, { scouter, schedule });
	}}>Go back</button
>

<style>
	main {
		display: flex;
		flex-direction: row;
		text-align: left;
		justify-content: space-around;
		align-items: flex-start;
		width: 100%;
		height: 100%;
	}
	.column {
		display: flex;
		flex-direction: column;
	}
	textarea {
		resize: none;
	}
</style>
