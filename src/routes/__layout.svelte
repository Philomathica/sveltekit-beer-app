<script lang="ts">
  import '../app.postcss';
  import { navigating, page } from '$app/stores';
  import Nav from '$lib/components/layout/Nav.svelte';
  import PreloadingIndicator from '$lib/components/ui/PreloadingIndicator.svelte';

  $: section = $page.path.split('/')[1];
</script>

<div>
  <div class="container mx-auto p-4">
    {#if $navigating}
      <PreloadingIndicator />
    {/if}

    <Nav {section} />

    <main>
      <slot />
    </main>
  </div>
</div>
