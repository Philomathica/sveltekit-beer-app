<script lang="ts">
  import { path } from '$lib/stores/layout/layout-store';
</script>

<nav class="p-4">
  <ul class="flex gap-2">
    <li><a sveltekit:prefetch href="/" class:active={$path === 'home'}>Home</a></li>
    <li><a sveltekit:prefetch href="/beers" class:active={$path === 'beers'}>Beers</a></li>
  </ul>
</nav>

<style lang="postcss">
  .active {
    @apply bg-blue-400 text-blue-100 underline;
  }
</style>
