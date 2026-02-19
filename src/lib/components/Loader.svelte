<script lang="ts">
  import { onMount } from 'svelte';

  let percent = 0;
  let showWe = false;
  let showAre = false;
  let showPage = false;

  onMount(() => {
    const interval = setInterval(() => {
      if (percent < 100) {
        percent += 1;
      } else {
        clearInterval(interval);
        // affichage progressif des textes
        setTimeout(() => showWe = true, 200);
        setTimeout(() => showAre = true, 800);
        setTimeout(() => showPage = true, 2000); // après 2s, afficher la page
      }
    }, 50);
  });
</script>

<style>
  .loader-container {
    display: flex;
    justify-content: center;
    align-items: flex-start;
    height: 100vh;
    position: absolute;
    top: 0; left: 0; right: 0; bottom: 0;
    background: white;
    z-index: 10;
  }

  .bar {
    width: 12px;
    height: 80%;
    background-color: #ccc;
    position: relative;
    border-radius: 3px;
    margin: 60px 60px; /* espace pour les textes */
  }

  .fill {
    position: absolute;
    top: 0;
    width: 100%;
    background-color: #1c168d;
    transition: height 0.05s linear;
    border-radius: 3px 3px 0 0;
  }

  .percent-label {
    position: absolute;
    left: 50%;
    transform: translateX(-50%) translateY(-50%);
    font-weight: bold;
    color: #1c168d;
    background: white;
    padding: 0 5px;
    border-radius: 3px;
    transition: top 0.05s linear;
  }

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

  .hidden {
    visibility: hidden;
    opacity: 0;
    transition: opacity 0.5s ease;
  }

  .visible {
    visibility: visible;
    opacity: 1;
    transition: opacity 0.5s ease;
  }

  .homepage {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
    font-size: 64px;
    font-weight: bold;
  }
</style>

{#if !showPage}
  <div class="loader-container">
    <!-- Textes WE / ARE -->
    <div class="text-container">
      <span class={showWe ? 'visible' : 'hidden'}>WE</span>
      <span class={showAre ? 'visible' : 'hidden'}>ARE</span>
    </div>

    <!-- Barre verticale -->
    <div class="bar">
      <div class="fill" style="height: {percent}%"></div>
      <div class="percent-label" style="top: {percent}%">{percent}%</div>
    </div>
  </div>
{/if}

{#if showPage}
  <div class="homepage">
    Vagabond Studio !
  </div>
{/if}
