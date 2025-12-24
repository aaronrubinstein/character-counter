<script lang="ts">
	import favicon from '$lib/assets/favicon.svg';
	import { browser } from '$app/environment';
	import '$lib/app.css';
	import Sun from '$lib/components/icons/Sun.svelte';
	import Moon from '$lib/components/icons/Moon.svelte';

	let { children } = $props();

	let darkMode = $state((browser && localStorage.getItem('theme') === 'dark') || false);

	const toggleTheme = () => {
		let newTheme = darkMode ? 'light' : 'dark';
		localStorage.setItem('theme', newTheme);
		document.body.setAttribute('data-theme', newTheme);
		darkMode = newTheme === 'dark';
	};

	const test = () => {
		console.log('test');
	};
</script>

<svelte:head>
	<title>Character Counter</title>
	<link rel="icon" href={favicon} />
	<link rel="preconnect" href="https://fonts.googleapis.com" />
	<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin="anonymous" />
	<link
		href="https://fonts.googleapis.com/css2?family=DM+Sans:ital,opsz,wght@0,9..40,100..1000;1,9..40,100..1000&display=swap"
		rel="stylesheet"
	/>
</svelte:head>

<div class="content">
	<header>
		{#if darkMode}
			<img class="logo" src="/logo-dark-theme.svg" alt="Character Counter Logo" />
			<button type="button" onclick={toggleTheme}>
				<Sun />
			</button>
		{:else}
			<img class="logo" src="/logo-light-theme.svg" alt="Character Counter Logo" />
			<button type="button" onclick={toggleTheme}>
				<Moon />
			</button>
		{/if}
	</header>

	{@render children()}
</div>

<style>
	.content {
		max-width: 990px;
		margin: 34px auto;
		padding: 0 32px;
	}

	header {
		display: flex;
		justify-content: space-between;
		align-items: center;
	}

	button {
		width: 44px;
		height: 44px;
		display: grid;
		place-items: center;
		border-radius: 8px;
		background: var(--input-bg);
	}

	@media (width < 1070px) {
		.content {
			margin: 16px auto;
		}
	}

	@media (width < 768px) {
		.content {
			margin: 16px auto;
			padding: 0 16px;
		}

		img.logo {
			height: 30px;
		}
	}
</style>
