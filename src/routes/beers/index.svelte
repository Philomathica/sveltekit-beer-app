<script lang="ts" context="module">
  import type { LoadInput, LoadOutput } from '@sveltejs/kit';
  import type { Beer } from '$lib/interfaces/beer';
  import { beerEndpoint } from '$lib/constants/constants';

  export async function load({ fetch, page }: LoadInput): Promise<LoadOutput> {
    const pageNumber = page.query.get('pageNumber') || '1';
    const pageSize = page.query.get('pageSize') || '20';
    const queryString = new URLSearchParams({ page: pageNumber, per_page: pageSize });
    const url = `${beerEndpoint}/beers?${queryString.toString()}`;
    const res: Response = await fetch(url);
    const beers: Beer[] = await res.json();

    if (res.ok) {
      return { props: { beers, pageNumber, pageSize } };
    }

    return { status: res.status, error: new Error(`Could not load ${url}`) };
  }
</script>

<script lang="ts">
  import { goto } from '$app/navigation';
  import BeerSummary from '$lib/components/beers/BeerSummary.svelte';

  export let beers: Beer[];
  export let pageNumber: string;
  export let pageSize: string;

  const pageSizes = ['20', '50', '80'];
  const pageNumbers = new Array(20).fill(null).map((x, i) => (i + 1).toString());

  function search() {
    const queryString = new URLSearchParams({ pageNumber, pageSize });
    goto(`/beers?${queryString.toString()}`, { noscroll: true });
  }
</script>

<svelte:head>
  <title>Beer App - Overview</title>
</svelte:head>

<header class="bg-white shadow py-6 px-8">
  <h1 class="text-3xl font-bold text-gray-900">Beer Overview</h1>
</header>

<div class="bg-white shadow mt-4 py-6 px-8">
  <label for="pageSize">Pagesize:</label>
  <select name="pageSize" bind:value={pageSize} on:change={search}>
    {#each pageSizes as pageSize}
      <option value={pageSize}>{pageSize}</option>
    {/each}
  </select>

  <label for="pageNumber">Pagenumber:</label>
  <select name="pageNumber" bind:value={pageNumber} on:change={search}>
    {#each pageNumbers as pageNumber}
      <option value={pageNumber}>{pageNumber}</option>
    {/each}
  </select>
</div>

<div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4 mt-4">
  {#each beers as beer (beer.id)}
    <BeerSummary {beer} />
  {/each}
</div>
