<script lang="ts">
	import Header from './Header.svelte';

	let formState = $state({
		answers: {} as Record<string, string>,
		step: 0,
		errors: ''
	});

	const QUESTIONS = [
		{
			question: 'Whats your name',
			id: 'name',
			type: 'text'
		},
		{
			question: 'Whats your birthday',
			id: 'birthday',
			type: 'date'
		},
		{
			question: 'Whats your fav color',
			id: 'color',
			type: 'color'
		}
	] as const;

	function nextStep(id: string) {
		if (formState.answers[id]) {
			formState.step++;
			formState.errors = '';
		} else {
			formState.errors = `${id} is required`;
		}
	}
</script>

<Header name={formState.answers.name} />

<main>
	{#if formState.step >= QUESTIONS.length}
		<p>Thank you for your answers</p>
	{:else}
		<p>Step: {formState.step + 1}</p>
	{/if}
	{#each QUESTIONS as { question, id, type }, index (id)}
		{#if formState.step === index}
			{@render formStep({ question, id, type })}
		{/if}
	{/each}

	{#if formState.errors}
		<p class="error">{formState.errors}</p>
	{/if}
</main>

<!-- {JSON.stringify(formState)} -->

{#snippet formStep({ question, id, type }: { question: string; id: string; type: string })}
	<article>
		<div>
			<label for={id}>{question}</label>
			<input {type} {id} bind:value={formState.answers[id as keyof typeof formState]} />
		</div>
		<button onclick={() => nextStep(id)}>Next</button>
	</article>
{/snippet}

<style>
	.error {
		color: red;
		font-size: 12px;
	}
</style>
