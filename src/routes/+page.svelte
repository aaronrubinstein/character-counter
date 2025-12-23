<script lang="ts">
	import Checkbox from '$lib/components/Checkbox.svelte';
	import StatCard from '$lib/components/StatCard.svelte';
	import Textarea from '$lib/components/Textarea.svelte';

	let text = $state('');
	let error: string | undefined = $state();
	let excludeSpaces = $state(false);
	let setCharacterLimit = $state(false);
	let characterLimit: number | undefined = $state();
	let charLimitElement: HTMLInputElement | undefined = $state();
	let charLimitMirror: HTMLSpanElement | undefined = $state();

	let characterCount = $derived.by(() => {
		if (excludeSpaces) {
			return text.replace(/\s/g, '').length;
		} else {
			return text.length;
		}
	});

	let wordCount = $derived((text.match(/\b\w+\b/g) || []).length);

	let sentenceCount = $derived.by(() => {
		const trimmedStr = text.trim();
		if (trimmedStr.length == 0) return 0;
		const sentenceEndings = trimmedStr.match(/[.!?]+/g);
		if (!sentenceEndings) return 1;
		return sentenceEndings.length;
	});

	let readingTimeMins = $derived(wordCount / 200);

	// Autosize character limit input
	$effect(() => {
		void characterLimit; // effect should rerun anytime character limit changes
		if (!charLimitMirror || !charLimitElement) return;
		let inputWidth = charLimitMirror.offsetWidth;
		if (inputWidth > 55) {
			charLimitElement.style.width = inputWidth + 'px';
		} else {
			charLimitElement.style.width = '55px';
		}
	});
</script>

<main>
	<h1>
		Analyze your text<br />
		in real-time
	</h1>

	<Textarea bind:value={text} {error} />

	<div class="options-container">
		<div class="options-checkboxes">
			<Checkbox bind:checked={excludeSpaces} label="Exclude Spaces" />
			<div class="character-limit">
				<Checkbox bind:checked={setCharacterLimit} label="Set Character Limit" />
				{#if setCharacterLimit}
					<input
						bind:this={charLimitElement}
						type="number"
						aria-label="Character limit"
						bind:value={characterLimit}
					/>
					<span
						bind:this={charLimitMirror}
						style="visibility: hidden; position: absolute; white-space: no-wrap; padding: 4px 12px;"
						>{characterLimit}</span
					>
				{/if}
			</div>
		</div>
		{#if readingTimeMins === 0}
			<span>Approx. reading time: 0 minutes</span>
		{:else if readingTimeMins < 1}
			<span>Approx. reading time: &lt; 1 minute</span>
		{:else if Math.round(readingTimeMins) < 2}
			<span>Approx. reading time: 1 minute</span>
		{:else}
			<span>Approx. reading time: {Math.round(readingTimeMins)} minutes</span>
		{/if}
	</div>

	<div class="stat-cards">
		<StatCard type="characters" count={characterCount} />
		<StatCard type="words" count={wordCount} />
		<StatCard type="sentences" count={sentenceCount} />
	</div>
</main>

<style>
	h1 {
		font-size: 64px;
		font-weight: 700;
		line-height: 100%;
		letter-spacing: -1px;
		color: var(--title-text);
		margin: 48px 0;
		text-align: center;
	}

	.options-container {
		height: 29px;
		margin-top: 16px;
		display: flex;
		justify-content: space-between;
		align-items: center;
		font-size: 16px;
		font-weight: 400;
		line-height: 130%;
		letter-spacing: -0.6px;
		color: var(--primary-text);
	}

	.options-checkboxes {
		display: flex;
		align-items: center;
		gap: 24px;
	}

	.character-limit {
		display: flex;
		align-items: center;
		gap: 10px;
	}

	input {
		outline: none;
		/* min-width: 55px; */
		padding: 4px 12px;
		border-radius: 6px;
		border: 1px solid var(--character-limit-input-border);
		color: var(----character-limit-input-text);
		font-size: 16px;
		font-weight: 400;
		line-height: 130%;
		letter-spacing: -0.6px;
		text-align: center;
	}

	.stat-cards {
		margin-top: 48px;
		display: flex;
		gap: 16px;
	}

	@media (width < 768px) {
		h1 {
			font-size: 40px;
		}
		br {
			display: none;
		}
	}
</style>
