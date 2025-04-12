<script lang="ts">
	import Header from './Header.svelte';

	let formState = $state({
		name: '',
		birthday: '',
		step: 0,
		errors: ''
	});
</script>

<Header name={formState.name} />

<main>
	<p>Step: {formState.step + 1}</p>

	{#if formState.step === 0}
		<div>
			<label for="name">Enter your Name</label>
			<input type="text" id="name" bind:value={formState.name} />
			{#if formState.errors}
				<p class="error">{formState.errors}</p>
			{/if}
		</div>
		<button
			onclick={() => {
				if (formState.name !== '') {
					formState.step++;
					formState.errors = '';
				} else {
					formState.errors = 'Name is required';
				}
			}}>Next</button
		>
	{:else if formState.step === 1}
		<div>
			<label for="bday">Enter your Birthday</label>
			<input type="date" id="bday" bind:value={formState.birthday} />
			{#if formState.errors}
				<p class="error">{formState.errors}</p>
			{/if}
		</div>
		<button
			onclick={() => {
				if (formState.birthday !== '') {
					formState.step++;
					formState.errors = '';
				} else {
					formState.errors = 'Birthday is required';
				}
			}}>Next</button
		>
	{:else}
		<p>Thank you</p>
	{/if}
</main>

<style>
	.error {
		color: red;
		font-size: 12px;
	}

	:global(div) {
		background-color: #f0f0f0;
	}
</style>
