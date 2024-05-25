<script>
	let init,
		x,
		y,
		p,
		step,
		d,
		zatvor = `G01 F1000 Z0<br>\nG01 F1000 Z10<br>\n`;

	let rez;
	let rezready = false;
	let xmatrix = [];
	let xmatrixreverse = [];
	let ymatrix = [];
	let ymatrixreverse = [];

	const even = (n) => !(n % 2);
	init = `G01 F2222 X0<br>\nG04 P3<br>\nG01 F2222 Y0<br>\nG04 P3<br>\n`
	const calculate = (init, x, y, p, step, d, zatvor) => {
		let xcount = Math.floor(x / step) + 1;
		let ycount = Math.floor(y / step) + 1;

		xmatrix.length = xcount;
		for (let index = 0; index < xmatrix.length; index++) {
			xmatrix[index] = index + 1;
			xmatrixreverse[index] = xcount - index;
		}

		ymatrix.length = ycount;
		for (let index = 0; index < ymatrix.length; index++) {
			ymatrix[index] = index + 1;
			ymatrixreverse[index] = ycount - index;
		}

		rez = init + '<br>\n';

		for (let index = 1; index < ycount; index++) {
			if (!even(index)) {
				for (let i = 0; i < xmatrix.length; i++) {
					const element = xmatrix[i];
					let token = '';
					let ntoken = '';

					ntoken = element * step;

					token = `G01 F${d} X${ntoken}<br>\nG04 P${p}<br>\n`;
					token = token + zatvor;
					rez = rez + token;
					rez = rez + `<br>\n`;
				}
			} else {
				for (let i = 0; i < xmatrixreverse.length; i++) {
					const element = xmatrixreverse[i];
					let token = '';
					let ntoken = '';

					ntoken = element * step;

					token = `G01 F${d} X${ntoken}<br>\nG04 P${p}<br>\n`;
					token = token + zatvor;
					rez = rez + token;
					rez = rez + `<br>\n`;
				}
			}

			let ytoken = '';
			let yntoken = '';

			yntoken = index * step;
			ytoken = `G01 F${d} Y${yntoken}<br>\nG04 P3<br>\n`;
			rez = rez + ytoken;
			rez = `<br>\n` +rez + `<br>\n`;
		}

		console.log(rez);

		rezready = true;
	};
</script>

<svelte:head>
	<title>Home</title>
	<meta name="description" content="Svelte demo app" />
</svelte:head>

<section>
	{#if !rezready}
		<div class="inp">
			<div class="sp">Инициализация</div>
			<textarea rows="4" bind:value={init} />
		</div>
		<div class="inp">
			<div class="sp">Длина</div>
			<input bind:value={x} />
		</div>
		<div class="inp">
			<div class="sp">Ширина</div>
			<input bind:value={y} />
		</div>
		<div class="inp">
			<div class="sp">Пауза</div>
			<input bind:value={p} />
		</div>
		<div class="inp">
			<div class="sp">Шаг</div>
			<input bind:value={step} />
		</div>
		<div class="inp">
			<div class="sp">Cкорость</div>
			<input bind:value={d} />
		</div>

		<div class="inp">
			<div class="sp">Команда затвора</div>
			<textarea rows="4" bind:value={zatvor} />
		</div>

		<button class="btn" on:click={calculate(init, x, y, p, step, d, zatvor)}>Go</button>
	{/if}
	{#if rezready}
		{@html rez}
	{/if}
</section>

<style>
	section {
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		flex: 0.6;
	}
	.sp {
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
