<script>
    import {pokemon} from "../stores/pokestore";
    import PokemanCard from "../components/pokemanCard.svelte";

    let searchTerm = "";
    let filteredPokemon = [];

    $:{
        console.log(searchTerm);

        if(searchTerm){
            //filter results
            filteredPokemon = $pokemon.filter(pokeman => pokeman.name.toLowerCase().includes(searchTerm.toLowerCase()));

        }else{
            filteredPokemon = [... $pokemon]; //makes a copy of the pokemon array
        }
    }
</script>
<svelte:head>
    <title>Svelte Kit Pokedex</title>
</svelte:head>
<h1 class="text-4xl text-center my-8 uppercase">Svelte Kit Pokedex</h1>

<!--filtered search-->
<input type="text" placeholder="Search Pokemon" class="w-full rounded-md text-lg p-4 border-2 border-gray-200" bind:value={searchTerm}>

<!-- parent container-->
<div class="py-4 grid gap-4 md:grid-cols-2 grid-cols-1"> 
    {#each filteredPokemon as pokeman}
        <PokemanCard pokeman={pokeman} />
    {/each}
</div>
<!-- end parent container-->