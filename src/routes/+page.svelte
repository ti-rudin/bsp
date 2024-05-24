<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	let x,y,z,s,d = "";

	let rez = ""

	const calculate = (x,y,z,s,d) => {
		console.log(Number(x)+Number(y)+Number(z));
		rez = Number(x)+Number(y)+Number(z)+Number(s)+Number(d)
	}

</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	
	
	<input bind:value={x}/>
	<input bind:value={y}/>
	<input bind:value={z}/>
	<input bind:value={s}/>
	<input bind:value={d}/>

	<button on:click={calculate(x,y,z,s,d)}>Go</button>

	<p>{rez}</p>
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}

	h1 {
		width: 100%;
	}

	.welcome {
		display: block;
		position: relative;
		width: 100%;
		height: 0;
		padding: 0 0 calc(100% * 495 / 2048) 0;
	}

	.welcome img {
		position: absolute;
		width: 100%;
		height: 100%;
		top: 0;
		display: block;
	}
</style>
