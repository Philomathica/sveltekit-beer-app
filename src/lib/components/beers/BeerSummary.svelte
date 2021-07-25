<script lang="ts">
	import type { Beer } from '$lib/interfaces/beer';

	export let beer: Beer;
</script>

<div class="p-4 rounded-md shadow-md bg-gray-100">
	<a href="/beers/{beer.id}" class="underline">
		<h4 class="font-bold">{beer.name}</h4>
	</a>

	<p>{beer.description}</p>

	<img width="80" height="80" src={beer.image_url} alt={beer.name} />
</div>
