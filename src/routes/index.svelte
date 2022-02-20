<script>
	import Guess from '$lib/Guess.svelte';
	import Top from '$lib/top.svelte';
	import { No, dict, Some, Exact } from '$lib/solver';

	let words = dict([]);

	function click(e) {
		let criteria = [];

		let grays = document.getElementById('gray').value.split('').map(v => v.toLowerCase());
		// Get all yellow fields
		let yellows = [1, 2, 3, 4, 5].map((v) => document.getElementById(`yellow-${v}`).value.toLowerCase());
		// Get all green fields
		let greens = [1, 2, 3, 4, 5].map((v) => document.getElementById(`green-${v}`).value.toLowerCase());

		grays.forEach((v) => {
			criteria.push(new No(v));
		});

		yellows.forEach((v, i) => {
			if (v != '') {
				criteria.push(new Some(v, i));
			}
		});

		greens.forEach((v, i) => {
			if (v != '') {
				criteria.push(new Exact(v, i));
			}
		});

		words = dict(
			criteria,
			words
		)
	}
</script>

<style lang="postcss">
	.green_box {
		@apply border-8 rounded-xl border-green-300 m-3 text-7xl w-[112px] font-extrabold shadow-md text-center uppercase;
	}

	.yellow_box {
		@apply border-8 rounded-xl border-yellow-300 m-3 text-7xl w-[112px] font-extrabold shadow-md text-center uppercase;
	}
</style>

<div class="flex justify-center items-center w-full flex-col">
	<h1 class="text-2xl mx-auto">
		<span class="text-gray-600">Gray</span>
		letters:
	</h1>

	<input
		type="text"
		name="grays"
		id="gray"
		class="border-8 rounded-xl border-gray-300 m-3 text-7xl w-1/2 mx-auto font-extrabold shadow-md uppercase"
	/>

	<br />

	<h1 class="text-2xl mx-auto">
		<span class="text-yellow-400">Yellow</span>
		letters:
	</h1>

	<!-- Done like this because positional info is necessary -->
	<div class="flex mx-auto w-4/5 translate-x-[20%]">
		<input
			type="text"
			name="yellow-1"
			id="yellow-1"
			class="yellow_box"
		/>
		<input
			type="text"
			name="yellow-2"
			id="yellow-2"
			class="yellow_box"
		/>
		<input
			type="text"
			name="yellow-3"
			id="yellow-3"
			class="yellow_box"
		/>
		<input
			type="text"
			name="yellow-4"
			id="yellow-4"
			class="yellow_box"
		/>
		<input
			type="text"
			name="yellow-5"
			id="yellow-5"
			class="yellow_box"
		/>
	</div>

	<br />

	<h1 class="text-2xl mx-auto">
		<span class="text-green-400">Green</span>
		letters:
	</h1>

	<div class="flex mx-auto w-4/5 translate-x-[20%]">
		<input
			type="text"
			name="green-1"
			id="green-1"
			class="green_box"
		/>
		<input
			type="text"
			name="green-2"
			id="green-2"
			class="green_box"
		/>
		<input
			type="text"
			name="green-3"
			id="green-3"
			class="green_box"
		/>
		<input
			type="text"
			name="green-4"
			id="green-4"
			class="green_box"
		/>
		<input
			type="text"
			name="green-5"
			id="green-5"
			class="green_box"
		/>
	</div>

	<br />

	<button
		type="button"
		on:click={click}
		class="text-7xl bg-blue-300 rounded-xl p-3 m-3 mx-auto w-1/3 font-extrabold shadow-md">Try</button
	>
	<br />
</div>

<div class="flex flex-wrap">
	<Top word={words.shift() ?? "Looks like we're stumped!"} />

	{#each words as word}
		<Guess {word} />
	{/each}
</div>
