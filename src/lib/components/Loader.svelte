<script lang="ts">
  import { onMount } from 'svelte';

  let percent = 0;

  onMount(() => {
    const interval = setInterval(() => {
      if (percent < 100) {
        percent += 1; // augmente de 1% à chaque tick
      } else {
        clearInterval(interval);
      }
    }, 50); // 50ms par tick → environ 5 secondes pour 100%
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
    width: 12px; /* barre fine */
    height: 100%;
    background-color: #ccc;
    position: relative;
    border-radius: 3px;
  }

  .fill {
    position: absolute;
    bottom: 0;
    width: 100%;
    background-color: #4f46e5; /* couleur stylée */
    transition: height 0.05s linear;
    border-radius: 3px 3px 0 0;
  }

  .percent-label {
    position: absolute;
    left: 50%;
    transform: translateX(-50%) translateY(50%);
    font-weight: bold;
    color: #4f46e5;
    background: white;
    padding: 0 5px;
    border-radius: 3px;
    transition: bottom 0.05s linear;
  }
</style>

<div class="loader-container">
  <div class="bar">
    <div class="fill" style="height: {percent}%"></div>
    <div class="percent-label" style="bottom: {percent}%">{percent}%</div>
  </div>
</div>
