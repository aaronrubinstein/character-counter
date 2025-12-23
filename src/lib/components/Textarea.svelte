<script lang="ts">
	let { value = $bindable(), error }: { value: string; error: string | undefined } = $props();
</script>

<div class="wrapper">
	<textarea
		name="input-text"
		id="input-text"
		placeholder="Start typing here... (or paste your text)"
		aria-label="Input your text here"
		aria-invalid={error ? 'true' : undefined}
		class:invalid={error}
	></textarea>
	{#if error}
		<div class="error-message">
			<img src="/icon-info.svg" alt="Error" />
			<span class="error-message-text">{error}</span>
		</div>
	{/if}
</div>

<style>
	textarea {
		outline: none;
		resize: vertical;
		width: 100%;
		height: 200px;
		padding: 20px;
		border-radius: 12px;
		border: 2px solid var(--input-border);
		background-color: var(--input-bg);
		font-size: 20px;
		font-weight: 400;
		line-height: 140%;
		letter-spacing: -0.6px;
		color: var(--secondary-text);
	}

	textarea:hover {
		background-color: var(--input-bg-hover);
		border: 2px solid var(--input-border-hover);
	}

	textarea:focus {
		background-color: var(--input-bg-focus);
		border: 2px solid var(--input-border-focus);
		box-shadow: 0 0 10px 0 var(--purple);
	}

	textarea.invalid {
		border: 2px solid var(--error);
		box-shadow: 0 0 8px 0 var(--error);
	}

	.error-message {
		display: flex;
		align-items: center;
		gap: 8px;
		margin-top: 12px;
	}

	.error-message-text {
		font-size: 16px;
		font-weight: 400;
		line-height: 130%;
		letter-spacing: -0.6px;
		color: var(--error);
	}
</style>
