<script lang="ts" context="module">
  import type { Beer } from '$lib/interfaces/beer';
  import type { LoadInput, LoadOutput } from '@sveltejs/kit';
  import { beerEndpoint } from '$lib/constants/constants';

  export async function load({ page: { params }, fetch }: LoadInput): Promise<LoadOutput> {
    const url = `${beerEndpoint}/beers/${params.id}`;
    const res: Response = await fetch(url);
    const beers: Beer[] = await res.json();

    if (res.ok && beers.length) {
      return { props: { beer: beers[0] } };
    }

    return { status: res.status, error: new Error(`Could not load ${url}`) };
  }
</script>

<script lang="ts">
  import BeerDetails from '$lib/components/beers/BeerDetails.svelte';

  export let beer: Beer;
</script>

<svelte:head>
  <title>Beer App - Details</title>
</svelte:head>

<h1 class="text-6xl">Beer Details</h1>

<div class="mt-4">
  <BeerDetails {beer} />
</div>
