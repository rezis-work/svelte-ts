<script lang="ts">
	import Header from './Header.svelte';

	let formState = $state({
		name: '',
		birthday: '',
		step: 0,
		errors: ''
	});
</script>

<Header name={formState.name}>
	<p>multi step form</p>
	{#snippet secondChildren(name: string)}
		<p>second children {name}</p>
	{/snippet}
</Header>

<main>
	<p>Step: {formState.step + 1}</p>

	{@render formStep({ question: 'Whats your name', id: 'name', type: 'text' })}

	{#if formState.step === 0}{/if}
</main>

{#snippet formStep({ question, id, type }: { question: string; id: string; type: string })}
	<article>
		<div>
			<label for={id}>{question}</label>
			<input {type} {id} bind:value={formState[id as keyof typeof formState]} />
		</div>
	</article>
{/snippet}

<style>
	/* .error {
		color: red;
		font-size: 12px;
	} */
</style>
