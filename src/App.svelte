<script>
	import { fade, fly } from "svelte/transition";
	import Checkbox from "./components/Checkbox.svelte";
	export let name;

	let list = [];
	let listVisible = false;

	const getItem = (min, max) => {
	  return { id: Math.random(), num: Math.floor(Math.random() * max + min) };
	};

	const addItem = () => {
	  list = [...list, getItem(0, 100)];
	};

	const add100Items = () => {
	  for (let n = 0; n < 100; n++) {
	    list = [...list, getItem(0, 100)];
	  }
	};

	const clearList = () => {
	  list = [];
	};

	const handleToggle = event => {
	  listVisible = event.detail;
	};
</script>

<style>
	h1 {
	  color: rgb(32, 12, 87);
	}
	ul {
	  list-style: none;
	}

	li {
	  font-size: 20px;
	  cursor: pointer;
	}

	#myList,
	#myTempText {
	  position: absolute;
	}

	#app {
	  position: relative;
	}
</style>

<div id="app">
	<h1>Hello {name}!</h1>
	<!-- <input type="checkbox" on:change={handleToggle}>Show list<br/> -->
	<Checkbox on:checked={handleToggle} />
	{#if listVisible===true}
		<div transition:fly="{{y:200, duration:500}}" id="myList">
			<h2>A list</h2>
			<button on:click={addItem}>Lägg till</button>
			<button on:click={add100Items}>Lägg till 100</button>
			<button on:click={clearList}>Rensa</button>
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
		{:else}
		<h2 id="myTempText" transition:fly="{{y:200, duration:500}}" >Check the chekcbox to see a list</h2>
	{/if}
</div>