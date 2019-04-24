<script>
	import { createEventDispatcher } from "svelte";
	import { fade } from "svelte/transition";

	let checked = false;

	const dispatch = createEventDispatcher();

	const checkMe = () => {
	  checked = !checked;
	  dispatch("checked", checked);
	};
</script>

<style>
	div {
	  color: rgb(0, 0, 0);
	  cursor: pointer;
	  user-select: none;
	  position: relative;
	  display: block;
	}

	img {
	  width: 20px;
	  position: absolute;
	  top: 0;
	}
</style>

<div>
	{#if checked===false}
		<img transition:fade on:click={checkMe} alt="" src="./Black_checkbox-unchecked.svg" />
	{:else}
		<img transition:fade on:click={checkMe} alt="" src="./Black_checkbox-checked.svg" />
	{/if}
</div>
<br/>