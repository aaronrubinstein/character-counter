<script lang="ts">
	let { checked = $bindable(), label }: { checked: boolean; label: string } = $props();
</script>

<label>
	<input type="checkbox" bind:checked />
	{label}
</label>

<style>
	label {
		display: flex;
		align-items: center;
		gap: 10px;
		font-size: 16px;
		font-weight: 400;
		line-height: 130%;
		letter-spacing: -0.6px;
		color: var(--primary-text);
	}

	input {
		appearance: none;
		width: 16px;
		height: 16px;
		border-radius: 4px;
		border: 1px solid var(--checkbox-border);
		cursor: pointer;
	}

	input:hover {
		border: 1px solid var(--checkbox-border-hover);
	}

	input:focus {
		outline: none;
		border: 1px solid var(--checkbox-border-focus);
		background-color: var(--checkbox-bg-focus);
		box-shadow:
			0 0 0 2px hsla(0, 0%, 100%, 1),
			0 0 0 4px var(--purple);
	}

	input:checked {
		border: 1px solid var(--checkbox-bg-checked);
		background-color: var(--checkbox-bg-checked);
		background-image: url('/icon-check.svg');
		background-repeat: no-repeat;
		background-position: center;
	}

	input:checked:hover {
		border: 1px solid var(--checkbox-bg-checked-hover);
		background-color: var(--checkbox-bg-checked-hover);
	}

	input:checked:focus {
		border: 1px solid var(--purple);
		background-color: var(--purple);
		box-shadow:
			0 0 0 2px hsla(0, 0%, 100%, 1),
			0 0 0 4px var(--purple);
	}
</style>
