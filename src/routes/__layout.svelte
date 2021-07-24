<script lang="ts">
	import '../app.postcss';
	import { navigating } from '$app/stores';
	import Nav from '$lib/layout/Nav.svelte';
</script>

<div class="container mx-auto px-4">
	<Nav />

	{#if $navigating}
		Loading...
	{/if}

	<main class="mt-12">
		<slot />
	</main>
</div>
