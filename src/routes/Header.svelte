<script lang="ts">
	let { name, fake_name = 'Rezi' }: { name: string; fake_name?: string } = $props();
</script>

<h1>Hello {name}</h1>
<h2>{name.replaceAll('r', 't').toUpperCase()}</h2>
<h3>Fake name: {fake_name}</h3>

<style>
	h3 {
		background-color: aqua;
	}
</style>
