<script lang="ts">
	import Checkbox from '$lib/components/Checkbox.svelte';
	import Textarea from '$lib/components/Textarea.svelte';

	let text = $state('');

	let characterCount = $derived.by(() => {
		if (excludeSpaces) {
			return text.replace(/\s/g, '').length;
		} else {
			return text.length;
		}
	});

	let wordCount = $derived.by(() => {});

	let sentenceCount = $derived.by(() => {});

	let error: string | undefined = $state();
	let excludeSpaces = $state(false);
	let setCharacterLimit = $state(false);
	let characterLimit: number | undefined = $state();
	let charLimitElement: HTMLInputElement | undefined = $state();
	let charLimitMirror: HTMLSpanElement | undefined = $state();

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
		Approx. reading time
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

	@media (width < 768px) {
		h1 {
			font-size: 40px;
		}
		br {
			display: none;
		}
	}
</style>
