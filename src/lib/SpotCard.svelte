<!-- src/lib/SpotCard.svelte -->

<script>
  // export let = this is a prop (data passed in from parent)
  export let name;
  export let location;
  export let waveType;
  export let difficulty;
  export let isFavourite = false; // default value
  export let onFavClick = () => {};

  // A lookup object: waveType string → colour hex
  const waveColors = {
    "Reef":        "#0ea5e9",
    "Beach Break": "#10b981",
    "Point Break": "#8b5cf6"
  };
</script>

<!-- Markup: plain HTML with {} for JS expressions -->
<div class="card">

  <div class="card-top" style="background: {waveColors[waveType]}">

    <span class="wave-type">{waveType}</span>

    <button on:click={onFavClick}>
      {isFavourite ? "♥" : "♡"}
    </button>

  </div>

  <div class="card-body">
    <h3>{name}</h3>
    <p>📍 {location}</p>

    <!-- Renders 5 dots. n <= difficulty = filled, rest = empty. -->
    {#each [1,2,3,4,5] as n}
      <span class={n <= difficulty ? "dot filled" : "dot"}></span>
    {/each}
  </div>
</div>

<style>
  /* Scoped! .card here ONLY affects SpotCard, nowhere else */
  .card { border-radius: 12px; border: 1px solid #e2e8f0; }
  .card-top    { display: flex; align-items: flex-start; justify-content: space-between; padding: 10px 12px; }
  .wave-type   { font-size: 11px; font-weight: 600; color: white; background: rgba(0,0,0,0.2); padding: 2px 8px; border-radius: 20px; }
  .card-body   { padding: 12px; }
  h3 { font-size: 15px; font-weight: 600; margin: 0 0 4px; color: #1e293b; }
  p { font-size: 12px; color: #64748b; margin: 0 0 10px; }
  .dot { width: 8px; height: 8px; border-radius: 50%; background: #e2e8f0; }
  .dot.filled { background: #0ea5e9; }
</style>
