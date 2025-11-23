<script>
	import { pb, store } from '$lib/store.svelte.js';
	import RabbitholeSelector from './RabbitholeSelector.svelte';

	let name = $state('');
	let rabbitholeId = $state();

	let wrongRabbitName = $derived(name.length > 0 && name[0] !== 'J');

	async function addRabbit() {
		await store.addRabbit(name, rabbitholeId);
		name = '';
		store.listRabbits();
	}
</script>

<div>
	<label for="name">Name</label>
	<input id="name" type="text" bind:value={name} class="input" />
</div>
<RabbitholeSelector setId={(id) => (rabbitholeId = id)}></RabbitholeSelector>
<button class="btn btn-primary" onclick={addRabbit} disabled={wrongRabbitName || name.length === 0}
	>Add Rabbit!</button
>
{#if wrongRabbitName}
	<div role="alert" class="mt-4 alert alert-error">
		<svg
			xmlns="http://www.w3.org/2000/svg"
			class="h-6 w-6 shrink-0 stroke-current"
			fill="none"
			viewBox="0 0 24 24"
		>
			<path
				stroke-linecap="round"
				stroke-linejoin="round"
				stroke-width="2"
				d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z"
			/>
		</svg>
		<span>Watch out! Rabbit names must start with "J"!</span>
	</div>
{/if}
