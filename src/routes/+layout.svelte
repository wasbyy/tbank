<script>
  import { onMount } from 'svelte';
</script>

<slot />

<style>
  /* Глобальные стили */
  :global(body) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: 'SF Pro Display', Arial, sans-serif;
  }
</style> 