<script lang="ts">
	import type { Beer } from '$lib/interfaces/beer';

	export let beer: Beer;
</script>

<div class="p-4 rounded-md shadow-md bg-gray-100">
	<h4 class="font-bold">{beer.name}</h4>

	<p>{beer.description}</p>

	<p class="font-bold mt-4">Yeast:</p>
	<p>{beer.ingredients.yeast}</p>

	<ul class="mt-4 font-bold">
		Malt:
		{#each beer.ingredients.malt as malt}
			<li class="font-normal list-disc list-inside">{malt.name}</li>
		{/each}
	</ul>

	<ul class="mt-4 font-bold">
		Hop:
		{#each beer.ingredients.hops as hop}
			<li class="font-normal list-disc list-inside">{hop.name}</li>
		{/each}
	</ul>

	<img class="mt-4" width="80" height="80" src={beer.image_url} alt={beer.name} />
</div>
