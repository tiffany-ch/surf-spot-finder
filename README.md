# Surf Spot Finder

A surf spot finder app that allows you to search for a surf spot around the world, providing information on the location, surf break, and difficulty.

## How it works

Search for a surf spot in the search bar and the corresponding results will come up. You can filter for difficulty levels, as well as save favorite spots into a 'Favorites' folder. 

## What I learnt from building a webpage using the Svelte framework:
**Set up**
- Using npm to create the project, install the relevant packages, and how to open a local browser.
- Distinguishing the relevant files within the package
-   src/lib/file-name.svelte
-   src/app.svelte
- File structure: (1) JS script at the top, (2) HTML, (3) CSS styling at the end

**Svelte concepts practised**
- Building a component with props, passing this to the parent file
- Creating state variables using *let*
- Reactive declarations using $: filtered = ...
- Rendering a list and adding search filtering using {#each: }
- Adding a dropdown filter to show a difficulty rating
- Using bindings to bind the (1) search bar input and (2) difficulty rating to the corresponding results
- Adding a 'favourites' feature with reactivity

