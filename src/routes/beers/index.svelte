<script lang="ts" context="module">
  import type { LoadInput, LoadOutput } from '@sveltejs/kit';
  import type { Beer } from '$lib/interfaces/beer';
  import { beerEndpoint } from '$lib/constants/constants';

  export async function load({ fetch }: LoadInput): Promise<LoadOutput> {
    const url = `${beerEndpoint}/beers`;
    const res: Response = await fetch(url);
    const beers: Beer[] = await res.json();

    if (res.ok) {
      return { props: { beers } };
    }

    return { status: res.status, error: new Error(`Could not load ${url}`) };
  }
</script>

<script lang="ts">
  import BeerSummary from '$lib/components/beers/BeerSummary.svelte';
  import { path } from '$lib/stores/layout/layout-store';

  export let beers: Beer[];

  path.set('beers');
</script>

<svelte:head>
  <title>Beer Overview</title>
</svelte:head>

<h1 class="text-6xl">Beer Overview</h1>

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-4">
  {#each beers as beer (beer.id)}
    <BeerSummary {beer} />
  {/each}
</div>
