<script lang="ts">
	import Header from './Header.svelte';

	let name = $state('rezi');
	let status: 'OPEN' | 'CLOSED' = $state('OPEN');
	let full_name = $derived(`${name} karanadze`);

	function onclick() {
		status = status === 'OPEN' ? 'CLOSED' : 'OPEN';
	}

	$effect(() => {
		console.log('status changed', status);
	});
</script>

<Header {name} fake_name="Rezi" />

<input type="text" bind:value={name} />

<h2>{full_name}</h2>

<p>The store is now {status}</p>

<button {onclick}>toggle status</button>
