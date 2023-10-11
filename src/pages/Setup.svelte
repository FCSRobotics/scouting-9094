<script lang="ts">
	import { onMount } from "svelte";
	import type { TeamGameData } from "../lib/types";

	export let setCurrentPage;

	let scouter: number | null = null;
	let schedule_text = "";

	function parseSchedule(
		raw: { schedule: any[] | null | undefined },
		scout: number
	): TeamGameData[] {
		let data = [] as TeamGameData[];
		if (raw.schedule == undefined || raw.schedule == null) return [];
		raw.schedule.forEach((match) => {
			data.push(
				...Object.keys(match.team_assignments)
					.filter((it) => match.team_assignments[it] == scout)
					.map(
						(it) =>
							({
								team: {
									number: it as string,
								},
								match_number: match.match_number as number,
								high_cones_auto: 0,
								mid_cones_auto: 0,
								low_cones_auto: 0,
								high_cubes_auto: 0,
								mid_cubes_auto: 0,
								low_cubes_auto: 0,
								mobility_auto: false,
								balanced_auto: 0,
								high_cones: 0,
								mid_cones: 0,
								low_cones: 0,
								high_cubes: 0,
								mid_cubes: 0,
								low_cubes: 0,
								defense: false,
								balanced: 0,
								parked: false,
								catastrophic_failure: false,
								sabotage: false,
								drive_grade: 0,
								overall_grade: 0,
								notes: "",
								done: false,
								won: false,
								exported: false,
							} as TeamGameData)
					)
			);
		});
		data.sort((a, b) => (a.match_number > b.match_number ? 1 : -1));
		console.log(data);
		return data;
	}
	let ls: Storage;
	onMount(() => {
		ls = localStorage;
	});

	let saved = "";
</script>

<label for="scouter_input">Input your scouter number:</label>
<input type="number" id="scouter_input" bind:value={scouter} />
{#if scouter != null}
	<p>&</p>
	<label for="schedule_input">Enter the schedule sent to you here:</label>
	<input type="text" id="schedule_input" bind:value={schedule_text} />
	<button
		on:click={() => {
			setCurrentPage(1, {
				scouter: scouter - 1,
				schedule: parseSchedule(JSON.parse(schedule_text), scouter - 1),
			});
		}}>Submit</button
	>
{/if}
<!-- <hr />
<p>or</p>

<label for="saved">Input previous saved data:</label>
<input type="text" name="saved" bind:value={saved} id="saved" />
<button
	on:click={() => {
		setCurrentPage(1, {
			schedule: JSON.parse(saved).schedule,
			scouter: JSON.parse(saved).scouter,
		});
	}}>Submit</button
> -->

<hr />
<p>or</p>
<button
	on:click={() => {
		setCurrentPage(1, {
			schedule: JSON.parse(ls.getItem("schedule")),
			scouter: parseInt(ls.getItem("scouter")),
		});
	}}>Continue from last session</button
>
