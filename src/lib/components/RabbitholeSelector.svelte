<script>
	import { pb } from '$lib/store.svelte';
	let { setId, id } = $props();
	let rabbitholes = $state([]);

	$effect(async () => {
		rabbitholes = await pb.collection('rabbitholes').getFullList();
	});
</script>

<div>
	<label for="name">Hasenbau</label>
	<select class="select" bind:value={id} onchange={() => setId(id)}>
		{#each rabbitholes as rabbithole (rabbithole.id)}
			<option value={rabbithole.id}>{rabbithole.name}</option>
		{/each}
	</select>
</div>
