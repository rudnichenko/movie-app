<script context="module">
  export async function load({fetch, params}){
    const res = await fetch(
      `https://api.themoviedb.org/3/search/movie?api_key=ef1291c77d80464afc7e37f8defd8556&language=en-US&query=${params.id}&page=1&include_adult=false`
    );
    const data = await res.json();
    if (res.ok){
      return{
        props: {searchedMovie: data.results}
      }
    }
  }
</script>

<script>
  import MovieCard from "../../components/MovieCard.svelte";
  export let searchedMovie;
</script>

<div class="searched-movies">
  {#each searchedMovie as movie}
    <MovieCard {movie} />
  {/each}
</div>

<style>
  .searched-movies {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
    grid-column-gap: .5rem;
    grid-row-gap: .5rem;
  }
</style>