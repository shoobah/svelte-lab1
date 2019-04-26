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

	$: getLines = () => {
	  let lines = [];
	  for (let x = 0; x < daysWidth; x += 1) {
	    for (let y = 0; y < hoursHeight; y += 24) {
	      lines.push({ x: x * xRatio, y: y * yRatio });
	    }
	  }
	  return lines;
	};

	const getTimeRect = (dtFrom, dtTo) => {
	  console.log("dtFrom, dtTo", { from: dtFrom.toISO(), to: dtTo.toISO() });
	  console.log("dtFrom.day / daysWidth", Math.floor(dtFrom.day / daysWidth));
	  console.log('dtTo.diff(dtFrom, "days")', dtTo.diff(dtFrom, "days").days);
	  console.log('dtTo.diff(dtFrom, "hours")', dtTo.diff(dtFrom, "hours").hours);
	  console.log("xRatio", xRatio);
	  console.log("yRatio", yRatio);
	  return {
	    x: dtFrom.weekday * xRatio,
	    width: Math.ceil(dtTo.diff(dtFrom, "days").days) * xRatio,
	    y: (Math.floor(dtFrom.day / daysWidth) * 24 + dtFrom.hour) * yRatio,

	    height: dtTo.diff(dtFrom, "hours").hours * yRatio
	  };
	};

	const from = DateTime.fromISO("2019-04-02T08:17:18.788+02:00", {
	  locale: "sv"
	});
	const to = from.plus({ hours: 6 });

	const test = {
	  from,
	  to,
	  rect: getTimeRect(from, to)
	};
	console.log("test", test);

	const handleDayClick = info => {
	  console.log(
	    `A meeting starting at ${from.toLocaleString()} lasting ${
	      to.diff(from, "minutes").minutes
	    } minutes`
	  );
	};
</script>

<style>
	.background {
	  fill: white;
	  stroke: black;
	}

	.day {
	  fill: lime;
	  stroke: none;
	  cursor: pointer;
	}
</style>

<div id="month-wrapper">
	<div>
	{DateTime.local()}<br/>
	<input type=range bind:value={width} min=25 max=1000 />
	</div>
	<svg height="80vh" width="80vh" viewBox="0 0 1000 1000" preserveAspectRatio xmlns="http://www.w3.org/2000/svg">
		<rect x="0" y="0" width={width} height={width} class="background" />
		{#each getLines() as line}
			<line x1="0" y1={line.y} x2={width} y2={line.y} stroke="black" />
			<line x1={line.x} y1=0 x2={line.x} y2={height} stroke="black" />
		{/each}
		<rect class="day" x={test.rect.x} y={test.rect.y} width={test.rect.width} height={test.rect.height} on:click={()=>{handleDayClick(test)}} />
	</svg>
</div>