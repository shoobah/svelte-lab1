<script>
	import { DateTime } from "luxon";
	const daysWidth = 7;
	const hoursHeight = 4 * 24;
	let width = 1000;
	let height = 1000;
	let xRatio = width / daysWidth;
	let yRatio = height / hoursHeight;

	$: height = width;

	$: xRatio = width / daysWidth;
	$: yRatio = height / hoursHeight;

	let lines = [];
	for (let x = 0; x < daysWidth; x += 1) {
	  for (let y = 0; y < hoursHeight; y += 24) {
	    lines.push({ x: x * xRatio, y: y * yRatio });
	  }
	}
</script>

<style>
	.background {
	  fill: white;
	  stroke: black;
	}

	.day {
	  fill: lime;
	  stroke: none;
	}
</style>

<div id="month-wrapper">
	<div>
	{DateTime.local()}
	<input type=range bind:value={width} max=1000 />
	</div>
	<svg height="80vh" width="100vw" viewBox="0 0 1000 1000" preserveAspectRatio xmlns="http://www.w3.org/2000/svg">
		<rect x="0" y="0" width={width} height={width} class="background" />
		{#each lines as line}
			<line x1="0" y1={line.y} x2={width} y2={line.y} stroke="black" />
			<line x1={line.x} y1=0 x2={line.x} y2={height} stroke="black" />
		{/each}
	</svg>
</div>