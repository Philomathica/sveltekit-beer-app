<script lang="ts" context="module">
  import type { LoadInput, LoadOutput } from '@sveltejs/kit';
  import type { Beer } from '$lib/interfaces/beer';
  import { beerEndpoint } from '$lib/constants/constants';

  export async function load({ fetch, page }: LoadInput): Promise<LoadOutput> {
    const queryString = new URLSearchParams({
      page: page.query.get('pageNumber') || '1',
      per_page: page.query.get('pageSize') || '20',
    });
    const url = `${beerEndpoint}/beers?${queryString.toString()}`;
    const res: Response = await fetch(url);
    const beers: Beer[] = await res.json();

    if (res.ok) {
      return { props: { beers } };
    }

    return { status: res.status, error: new Error(`Could not load ${url}`) };
  }
</script>

<script lang="ts">
  import { goto } from '$app/navigation';
  import BeerSummary from '$lib/components/beers/BeerSummary.svelte';
  import { path } from '$lib/stores/layout/layout-store';

  export let beers: Beer[];

  let pageNumber: string;
  let pageSize: string;

  path.set('beers');

  function search() {
    const queryString = new URLSearchParams({ pageNumber: pageNumber || '1', pageSize: pageSize || '20' });
    goto(`/beers?${queryString.toString()}`);
  }
</script>

<svelte:head>
  <title>Beer Overview</title>
</svelte:head>

<h1 class="text-6xl">Beer Overview</h1>

<input class="border" type="number" min="1" bind:value={pageNumber} placeholder="page number" />
<input class="border" type="number" min="1" bind:value={pageSize} placeholder="page size" />
<button class="border" on:click={search}>Search</button>

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-4">
  {#each beers as beer (beer.id)}
    <BeerSummary {beer} />
  {/each}
</div>
