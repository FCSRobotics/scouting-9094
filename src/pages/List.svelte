<script lang="ts">
  import type { TeamGameData } from "../lib/types";

  export let setCurrentPage;
  export let scouter: number;
  export let schedule = [] as TeamGameData[];
  $: (() => {
    localStorage.setItem("schedule", JSON.stringify(schedule));
    localStorage.setItem("scouter", scouter.toString());
  })();
  console.log(schedule[0]);

  function simplify(schedule: TeamGameData[]) {
    let output = schedule.filter((value) => value.done && !value.exported);
    schedule.forEach((value) =>
      value.done ? (value.exported = true) : "noop"
    );
    return chunks(output, 2);
  }

  const chunks = (a, size) =>
    Array.from(new Array(Math.ceil(a.length / size)), (_, i) =>
      a.slice(i * size, i * size + size)
    );
</script>

<header>
  <!-- <button
		on:click={() => {
			setCurrentPage(3, { text: JSON.stringify({ scouter, schedule }) });
		}}>View data</button
	> -->
  <button
    on:click={() => {
      setCurrentPage(4, {
        goBack: () => {
          setCurrentPage(1, { scouter, schedule });
        },
        content: simplify(schedule),
      });
    }}>View Qr</button
  >
</header>
<main>
  {#each schedule as match, i}
    <button
      class={`list-item ${match.done ? "done" : ""} ${
        match.exported ? "exported" : ""
      }`}
      on:click={() => {
        setCurrentPage(2, { index: i, schedule, scouter, setCurrentPage });
      }}
      ><p>Match: {match.match_number}</p>
      <p>{match.team.number}</p></button
    >
  {/each}
</main>

<style>
  main {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;
    background-color: #cae8b5;
  }
  .list-item {
    width: 100%;
    background-color: white;
    border: 1px solid black;
    transition: background-color 250ms;
    color: black;
  }

  .list-item:hover {
    background-color: rgb(211, 211, 211);
  }

  .done.exported {
    background-color: green;
    color: white;
  }

  .done.exported:hover {
    background-color: rgb(0, 95, 0);
    color: white;
  }

  .done {
    background-color: yellow;
    color: black;
  }

  .done:hover {
    background-color: rgb(194, 194, 0);
    color: black;
  }
</style>
