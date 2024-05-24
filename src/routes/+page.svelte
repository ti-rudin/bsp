<script>
	import Counter from './Counter.svelte';
	import welcome from '$lib/images/svelte-welcome.webp';
	import welcome_fallback from '$lib/images/svelte-welcome.png';
	let x,
		y,
		z,
		s,
		d = '';

	let rez = '';

	const calculate = (x, y, z, s, d) => {
		console.log(Number(x) + Number(y) + Number(z));
		rez = Number(x) + Number(y) + Number(z) + Number(s) + Number(d);
	};
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	<div class="inp">
		<div class="sp">Длина</div>
		<input bind:value={x} />
	</div>
	<div class="inp">
		<div class="sp">Ширина</div>
		<input bind:value={y} />
	</div>
	<div class="inp">
		<div class="sp">Глубина</div>
		<input bind:value={z} />
	</div>
	<div class="inp">
		<div class="sp">Шаг</div>
		<input bind:value={s} />
	</div>
	<div class="inp">
		<div class="sp">Cкорость</div>
		<input bind:value={d} />
	</div>
	

	<button class="btn" on:click={calculate(x, y, z, s, d)}>Go</button>

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
.sp{
	width: 3rem;
}
	.inp {
		display: block;
		margin: 5px;
	}
	.btn {
		margin: 5px;
	}
</style>
