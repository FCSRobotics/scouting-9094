<script lang="ts">
  export let setCurrentPage;
  export let scouter;
  let schedule = [];
  export let raw_schedule;
  $: schedule = parseSchedule(raw_schedule, scouter);

  function parseSchedule(raw, scout) {
    let data = [];
    if (raw.schedule == undefined || raw.schedule == null) return [];
    raw.schedule.forEach((match) => {
      console.log(match);
      console.log(match.team_assignments);
      data.push(
        Object.keys(match.team_assignments)
          .filter((it) => match.team_assignments[it] == scout)
          .map((it) => ({ team: it, match: match.match_number }))
      );
    });
    return data;
  }
</script>

<p>{JSON.stringify(schedule)}</p>
