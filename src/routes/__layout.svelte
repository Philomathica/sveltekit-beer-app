<script lang="ts">
  import '../app.postcss';
  import { navigating } from '$app/stores';
  import Nav from '$lib/components/layout/Nav.svelte';
</script>

<div class="container mx-auto p-4">
  <Nav />

  <div class={$navigating ? 'opacity-1' : 'opacity-0'}>Loading...</div>

  <main class="mt-12">
    <slot />
  </main>
</div>
