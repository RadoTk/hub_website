<script lang="ts">
  import './layout.css';
  import favicon from '$lib/assets/favicon.svg';
  import Loader from "$lib/components/Loader.svelte";
</script>

<svelte:head>
  <link rel="icon" href={favicon} />
</svelte:head>

<Loader />

<slot /> <!-- ici, tout le contenu des pages sera injecté -->
