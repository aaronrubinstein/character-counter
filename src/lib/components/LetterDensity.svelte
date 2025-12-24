<script lang="ts">
	let { character, count, percentage }: { character: string; count: number; percentage: number } =
		$props();
</script>

<div class="container">
	<span>{character}</span>
	<span>
		{`${count} (${new Intl.NumberFormat('default', {
			style: 'percent',
			minimumFractionDigits: 2,
			maximumFractionDigits: 2
		}).format(percentage)})`}
	</span>
</div>
