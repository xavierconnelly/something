<script context="module">
	let selected;
</script>

<script>
	
	import { INDEX, HOVER, stations } from './Stations.js'
	
	let clicked;	
	const unsubscribe = INDEX.subscribe(value => clicked = value);
	
	export let src;
	export let name;
	export let i;
	export let utc;
	
		let radius = 360 / stations.length;
		let Index = stations[0];
	
	let audio;
	let paused = true;
	let hovered = false;

	const handleClick = () => {
		 paused = !paused;
		INDEX.set(i);
	}
	
	const mouseOver = () => {
		hovered = true;
		HOVER.set(i);
	}
	
	const mouseOut = () => {
		hovered = true;
		HOVER[i] = INDEX;
	}
	
	// let INDEX = !paused
		
	function stopOthers() {
		if (selected && selected !== audio) selected.pause();
		selected = audio;
	}
</script>

<!-- height: calc(2 * 3.14px * {radius});-->

<article class="hand"
				 class:playing={!paused}
				 on:click={handleClick}
				 on:mouseenter={mouseOver}
					style="	transform: rotate(calc({i} * {radius}deg))
									translateX(50%);">
	<span class="details">
		<span class="name"
					>
			{name}
		</span>
		<span class="utc">
						{utc}
		</span>	
	</span>
		<audio  preload="none"
			bind:this={audio}
			bind:paused
			on:play={stopOthers}
			{src}>
		</audio>
</article>

<style>
	:global(body) {
		margin: 0;
		padding: 0;
		color: #F4F2EA;
		background: #453939;
}
	
.hand {
		height: 20px;
    line-height: 7px;
    background: #453939;
    width: 50%;
    position: absolute;
    /* left: calc(50% - 0px); */
    top: calc(50% - 10px);
	left: 25%;
    text-align: right;
    cursor: pointer;
    color: #F4F2EA;
    transform-origin: center;
	border-top: 1px solid white;
	mix-blend-mode: lighten;
}	
	
.details .name {
		padding-right: 5px;
		transition: 1s;
	font-size: 4px;
		will-change: transform;
}

.hand:hover .name  {
		font-size: 16px;
		opacity: 100%;
		transition: .2s;
		z-index: 99;
}

.details .utc {
		margin: 0;
		color:  #453939;
		position: absolute;
		top: 50%;
		-ms-transform: translateY(-50%);
		transform: translateY(-50%);
		width: 50px;
		height: 100%;
	/*border-top: 1px solid;*/
		z-index: 1;
}

.playing {color: #453939}

</style>
