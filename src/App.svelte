<script>
// Imports
import SpotCard from "./lib/SpotCard.svelte";

// JS array
let spots = [
    { id: 1, name: "Uluwatu",      location: "Bali, Indonesia",   waveType: "Reef",        difficulty: 4 },
    { id: 2, name: "Pipeline",     location: "Oahu, Hawaii",      waveType: "Reef",        difficulty: 5 },
    { id: 3, name: "Jeffreys Bay", location: "Eastern Cape, SA",  waveType: "Point Break", difficulty: 3 },
    { id: 4, name: "Big Wave Bay", location: "Hong Kong",  waveType: "Beach Break", difficulty: 1 },
    { id: 5, name: "Fistral Beach", location: "Newquay, UK",  waveType: "Beach Break", difficulty: 3 },
    { id: 6, name: "Riberia d'Ilhas", location: "Ericeira, Portugal",  waveType: "Beach Break", difficulty: 3 },    
];

// State variables
// When any of these change, Svelte re-renders only the parts of the UI that depend on them.
  let searchTerm = "";
  /** @type {any[]} */
  let favourites = [];
  let showFavsOnly = false;
  let selectedDifficulty = "all";


    // Reactive declaration
    // SearchTerm, selectedDifficulty, showFavsOnly, and favourites: if either changes, `filtered` recalculates.
 $: filtered = spots
    .filter(s => s.name.toLowerCase().includes(searchTerm.toLowerCase()))
    .filter(s => selectedDifficulty === "all" || s.difficulty === Number(selectedDifficulty))
    .filter(s => !showFavsOnly || isFav(s));

  // Functions 
  // Checks if a spot is in the favourites array.
  /**
   * @param {any} spot
   * @returns {boolean}
   */
  function isFav(spot) {
    return !!favourites.find(f => f.id === spot.id);
  }

  // Adds or removes a spot from favourites.
  /**
   * @param {any} spot
   */
  function toggleFav(spot) {
    if (isFav(spot)) {
      favourites = favourites.filter(f => f.id !== spot.id); // remove
    } else {
      favourites = [...favourites, spot];                     // add
    }
  }

</script>


<!-- Template -->
 <main>

<!-- HEADER: shows live counts, "saved only" toggle -->
  <header>
    <div>
      <h1>🏄 Surf Spot Finder</h1>
      <p>{filtered.length} spots · {favourites.length} saved</p>
    </div>
    
    <!-- Inline handler: flips showFavsOnly between true/false -->
    <button on:click={() => showFavsOnly = !showFavsOnly}>
      {showFavsOnly ? "Show all" : "Saved only"}
    </button>
  </header>

<!-- Filters -->
<input placeholder="Search spots..." bind:value={searchTerm} />

<!-- Changing this updates selectedDifficulty, triggering $: filtered -->
<select bind:value={selectedDifficulty}>
  <option value="all">All levels</option>
  <option value="1">Level 1</option>
  <option value="2">Level 2</option>
  <option value="3">Level 3</option>
  <option value="4">Level 4</option>
  <option value="5">Level 5</option>
</select>


<!-- CARD GRID ──────────────────────────────────────── -->
  <div class="grid">
    {#each filtered as spot (spot.id)}
      <SpotCard
        {...spot}
        isFavourite={isFav(spot)}
        onFavClick={() => toggleFav(spot)}
      />

    {:else}
      <p class="empty">No spots match your search.</p>
    {/each}

  </div>
</main>
