<script context="module">
  export async function load({fetch}){
    const res = await fetch(
    `https://api.themoviedb.org/3/movie/popular?api_key=ef1291c77d80464afc7e37f8defd8556&language=en-US&page=1`
    );
    const data = await res.json();
    
    if (res.ok){
      return{
        props: {popular: data.results}
      }
    }
  }
</script>

<script>
  import PopularMovies from "../components/PopularMovies.svelte";
import SearchMovies from "../components/SearchMovies.svelte";
  import SearchMovie from "../components/SearchMovies.svelte";
  export let popular;
</script>

<section>
  <SearchMovies />
  <PopularMovies {popular}/>
</section>