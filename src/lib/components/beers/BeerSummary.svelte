<script lang="ts">
  import type { Beer } from '$lib/interfaces/beer';
  import { fade } from 'svelte/transition';

  export let beer: Beer;
</script>

<div class="p-8 rounded-sm shadow bg-white" in:fade={{ duration: 500 }}>
  <a href="/beers/{beer.id}" class="underline">
    <h4 class="font-bold">{beer.name}</h4>
  </a>

  <p>{beer.description}</p>

  <img width="80" height="80" src={beer.image_url} alt={beer.name} />
</div>
