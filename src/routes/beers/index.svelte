<script lang="ts" context="module">
	import type { Beer } from '$lib/interfaces/beer';

	export async function load({ page, fetch, session, context }) {
		const baseUrl = 'https://api.punkapi.com/v2';
		const url = `${baseUrl}/beers`;
		const res = await fetch(url);
		const beers: Beer[] = await res.json();

		if (res.ok) {
			return { props: { beers } };
		}

		return { status: res.status, error: new Error(`Could not load ${url}`) };
	}
</script>

<script lang="ts">
	import BeerSummary from '$lib/beers/BeerSummary.svelte';

	export let beers: Beer[];
</script>

<div class="grid grid-cols-3 gap-4">
	{#each beers as beer (beer.id)}
		<BeerSummary {beer} />
	{/each}
</div>
