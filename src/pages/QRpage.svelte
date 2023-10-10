<script>
	import QrCode from "svelte-qrcode";
	export let content;

	export let goBack;
</script>

<button on:click={() => goBack()}>Back</button>

{#each content as code}
	<QrCode value={JSON.stringify(code)} />
	<p>{JSON.stringify(code)}</p>
{/each}
