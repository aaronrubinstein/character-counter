<script lang="ts">
	let { character, count, percentage }: { character: string; count: number; percentage: number } =
		$props();
</script>

<div class="container">
	<span class="character">{character}</span>
	<div class="bar">
		<div class="filled-bar" style="width: {percentage * 100}%"></div>
	</div>
	<span class="count">
		{`${count} (${new Intl.NumberFormat('default', {
			style: 'percent',
			minimumFractionDigits: 2,
			maximumFractionDigits: 2
		}).format(percentage)})`}
	</span>
</div>

<style>
	.container {
		display: flex;
		align-items: center;
		gap: 14px;
		font-size: 16px;
		font-weight: 400;
		line-height: 130%;
		letter-spacing: -0.6px;
		color: var(--primary-text);
		margin-bottom: 12px;
	}

	.character {
		flex: 0 0 16px;
	}

	.bar {
		position: relative;
		flex: 1 0 0;
		height: 12px;
		border-radius: 12px;
		background: var(--density-bar-bg);
	}

	.filled-bar {
		position: absolute;
		top: 0;
		left: 0;
		height: 12px;
		border-radius: 12px;
		background: var(--purple);
	}

	.count {
		flex: 0 0 100px;
	}
</style>
