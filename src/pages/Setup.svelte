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
		balanced_auto: number;
		high_cones: number;
		mid_cones: number;
		low_cones: number;
		high_cubes: number;
		mid_cubes: number;
		low_cubes: number;
		defense: boolean;
		balanced: number;
		parked: boolean;
		catastrophic_failure: boolean;
		sabotage: boolean;
		drive_grade: number;
		overall_grade: number;
		notes: string;
		team: Team;
		match_number: number;
		done: boolean;
		won: boolean;
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
					.map(
						(it) =>
							({
								team: { number: it as string },
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
							} as TeamGameData)
					)
			);
		});
		data.sort((a, b) => (a.match_number > b.match_number ? 1 : -1));
		console.log(data);
		return data;
	}

	let saved = "";
</script>

<input type="number" bind:value={scouter} />
{#if scouter != null}
	<h1>Enter the schedule sent to you here:</h1>
	<input type="text" bind:value={schedule_text} />
{/if}<button
	on:click={() => {
		setCurrentPage(1, {
			scouter,
			schedule: parseSchedule(JSON.parse(schedule_text), scouter),
		});
	}}>Click</button
>

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
>
