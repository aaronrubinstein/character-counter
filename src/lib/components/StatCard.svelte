<script lang="ts">
	let { count, type }: { count: number; type: 'characters' | 'words' | 'sentences' } = $props();
</script>

<div class={['card', type]}>
	<p class="count">{count}</p>
	{#if type === 'characters'}
		<p class="label">Total Characters</p>
	{:else if type === 'words'}
		<p class="label">Word Count</p>
	{:else}
		<p class="label">Sentence Count</p>
	{/if}
</div>

<style>
	.card {
		height: 150px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 5px;
		border-radius: 12px;
		padding: 16px;
		flex: 1 0 0;
	}

	.card.characters {
		background-color: var(--purple);
	}

	.card.words {
		background-color: var(--yellow);
	}

	.card.sentences {
		background-color: var(--orange);
	}

	.count {
		font-size: 64px;
		font-weight: 700;
		line-height: 100%;
		letter-spacing: -1px;
		color: hsla(233, 18%, 9%, 1);
	}

	.label {
		font-size: 20px;
		font-weight: 400;
		line-height: 140%;
		letter-spacing: -0.6px;
		color: hsla(233, 18%, 9%, 1);
	}
</style>
