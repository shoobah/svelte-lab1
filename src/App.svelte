<script>
	export let name;

	let list = [];

	const getNumber = (min, max) => {
	  return Math.floor(Math.random() * max + min);
	};

	const handleClick = () => {
	  list = [...list, getNumber(0, 100)].sort((a, b) =>
	    a < b ? -1 : a > b ? 1 : 0
	  );
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
<button on:click={handleClick}>Klicka</button>
<div>
<span>Length={list.length}</span>
	<ul>
		{#each list as item (item)}
			<li>
				{item}
			</li>
			{:else}
			<li>Tom</li>
		{/each}
	</ul>
</div>