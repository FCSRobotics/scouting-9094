<script lang="ts">
	import List from "./pages/List.svelte";

	// import QrCode from "svelte-qrcode";

	import Setup from "./pages/Setup.svelte";
	import TeamView from "./pages/TeamView.svelte";
	import ViewText from "./pages/ViewText.svelte";
	let scouter = 0;
	let currentPage = 0;
	let gameData = [];
	let schedule = [];
	let currentProps = {} as object;

	function convertSchedule(schedule_data, scouter) {}
</script>

<main>
	<!-- <QrCode value={JSON.stringify({ hello: "world" })} /> -->
	{#if currentPage == 0}
		<Setup
			setCurrentPage={(value, props) => {
				currentPage = value;
				currentProps = props;
			}}
			{...currentProps}
		/>
	{:else if currentPage == 1}
		<List
			setCurrentPage={(value, props) => {
				currentPage = value;
				currentProps = props;
			}}
			{...currentProps}
		/>
	{:else if currentPage == 2}
		<TeamView
			setCurrentPage={(value, props) => {
				currentPage = value;
				currentProps = props;
			}}
			{...currentProps}
		/>
	{:else if currentPage == 3}
		<ViewText
			setCurrentPage={(value, props) => {
				currentPage = value;
				currentProps = props;
			}}
			{...currentProps}
		/>
	{/if}
</main>

<style>
</style>
