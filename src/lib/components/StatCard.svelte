<script lang="ts">
	import patternCharacter from '$lib/assets/pattern-character-count.svg';
	import patternWord from '$lib/assets/pattern-word-count.svg';
	import patternSentence from '$lib/assets/pattern-sentence-count.svg';
	import NumberFlow from '@number-flow/svelte';

	let { count, type }: { count: number; type: 'characters' | 'words' | 'sentences' } = $props();
</script>

<div class={['card', type]}>
	<NumberFlow value={count} locales="en" format={{ minimumIntegerDigits: 2, useGrouping: true }} />
	<!-- <p class="count">{count}</p> -->
	{#if type === 'characters'}
		<p class="label">Total Characters</p>
		<img src={patternCharacter} alt="" />
	{:else if type === 'words'}
		<p class="label">Word Count</p>
		<img src={patternWord} alt="" />
	{:else}
		<p class="label">Sentence Count</p>
		<img src={patternSentence} alt="" />
	{/if}
</div>

<style>
	.card {
		height: 150px;
		display: flex;
		flex-direction: column;
		justify-content: center;
		gap: 0px;
		border-radius: 12px;
		padding: 16px;
		flex: 1 0 0;
		position: relative;
		overflow: hidden;
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

	:global(number-flow-svelte) {
		font-size: 64px;
		font-weight: 700;
		line-height: 100%;
		letter-spacing: -1px;
		color: hsla(233, 18%, 9%, 1);
		--number-flow-mask-height: 0.1em;
		position: relative;
		z-index: 2;
	}

	.label {
		font-size: 20px;
		font-weight: 400;
		line-height: 140%;
		letter-spacing: -0.6px;
		color: hsla(233, 18%, 9%, 1);
		position: relative;
		z-index: 2;
	}

	img {
		position: absolute;
		right: -32px;
		z-index: 1;
	}

	@media (width < 768px) {
		.card {
			flex: 0 1 auto;
		}

		:global(number-flow-svelte) {
			font-size: 40px;
			--number-flow-mask-height: 0.2em;
		}
	}
</style>
