<script lang="ts">
	import type { Snippet } from 'svelte';

	let {
		name,
		children,
		secondChildren
	}: { name: string; children: Snippet; secondChildren: Snippet } = $props();
</script>

<div>
	<h1>{name ? `${name}` : ''}</h1>
	{@render children()}

	<h3>{@render secondChildren(name)}</h3>
</div>
