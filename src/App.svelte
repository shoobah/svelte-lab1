<script>
	import { fade, fly } from "svelte/transition";
	export let name;

	let list = [];

	const getItem = (min, max) => {
	  return { id: Math.random(), num: Math.floor(Math.random() * max + min) };
	};

	const addItem = () => {
	  list = [...list, getItem(0, 100)];
	};

	const add100Items = () => {
	  for (let n = 0; n < 10000; n++) {
	    list = [...list, getItem(0, 100)];
	    // .sort((a, b) =>
	    //   a < b ? -1 : a > b ? 1 : 0
	    // );
	  }
	};

	const clearList = () => {
	  list = [];
	};
</script>

<style>
	h1 {
	  color: rgb(92, 117, 23);
	}
	ul {
	  list-style: none;
	}

	li {
	  font-size: 20px;
	  cursor: pointer;
	}
</style>

<h1>Hello {name}!</h1>
<button on:click={addItem}>Lägg till</button>
<button on:click={add100Items}>Lägg till 100</button>
<button on:click={clearList}>Rensa</button>
<div>
<span>Length={list.length}</span>
	<ul>
		{#each list as item (item.id)}
			<li>
				{item.num}
			</li>
			{:else}
			<li>Tom</li>
		{/each}
	</ul>
</div>