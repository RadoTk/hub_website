<script lang="ts">
  import { onMount } from 'svelte';
  import { fade } from 'svelte/transition';

  let percent = 0;
  let showWe = false;
  let showAre = false;

  onMount(() => {
    const interval = setInterval(() => {
      if (percent < 100) {
        percent += 1;
      } else {
        clearInterval(interval);
        // affichage progressif avec delay
        setTimeout(() => showWe = true, 200);
        setTimeout(() => showAre = true, 800);
      }
    }, 50);
  });
</script>

<style>
  .loader-container {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    height: 80vh;
    position: relative;
    margin: 50px auto;
  }

  .bar {
    width: 12px;
    height: 100%;
    background-color: #ccc;
    position: relative;
    border-radius: 3px;
    margin: 0 60px; /* espace pour texte */
  }

  .fill {
    position: absolute;
    bottom: 0;
    width: 100%;
    background-color: #1c168d;
    transition: height 0.05s linear;
    border-radius: 3px 3px 0 0;
  }

  .percent-label {
    position: absolute;
    left: 50%;
    transform: translateX(-50%) translateY(50%);
    font-weight: bold;
    color: #1c168d;
    background: white;
    padding: 0 5px;
    border-radius: 3px;
    transition: bottom 0.05s linear;
  }

  /* texte WE et ARE */
  .text-container {
    position: absolute;
    top: 0;
    bottom: 0;
    display: flex;
    align-items: center;
    justify-content: space-between;
    width: 60%;
    pointer-events: none;
    font-weight: bold;
    font-size: 32px;
  }
</style>

<div class="loader-container">
  <div class="text-container">
    {#if showWe}
      <span transition:fade={{ duration: 800, delay: 0 }}>WE</span>
    {/if}
    {#if showAre}
      <span transition:fade={{ duration: 800, delay: 0 }}>ARE</span>
    {/if}
  </div>

  <div class="bar">
    <div class="fill" style="height: {percent}%"></div>
    <div class="percent-label" style="bottom: {percent}%">{percent}%</div>
  </div>
</div>
