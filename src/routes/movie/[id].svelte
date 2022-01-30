<script context="module">
  export async function load({fetch, params}){
    const res = await fetch(
      `https://api.themoviedb.org/3/movie/${params.id}?api_key=${import.meta.env.VITE_API}&language=en-US`
    );
    const movieDetail = await res.json();
    
    if (res.ok){
      return{
        props: {movieDetail}
      }
    }
  }
</script>

<script>
  export let movieDetail;
  import { fly } from 'svelte/transition';
</script>

<div class="movie-details" in:fly={{ y: 50, duration: 500, delay: 500 }} out:fly={{ duration: 500 }}>
  <div class="img-container">
    <img src={'https://image.tmdb.org/t/p/original' + movieDetail.backdrop_path} alt={movieDetail.title}>
  </div>
  <div class="txt-container">
    <h1>{movieDetail.title}</h1>
    <p class="overview">{movieDetail.overview}</p>
    <div>
      <div class="inf"><span>Release date: </span>
      {movieDetail.release_date}<br></div>
      <div class="inf"><span>Budget:</span> ${movieDetail.budget}<br></div>
      <div class="inf"><span>Rating:</span>
      {movieDetail.vote_average}<br></div>
      <div class="inf"><span>Runtime:</span>
      {movieDetail.runtime}mins</div>
    </div>
  </div>
</div>

<style>
  h1 {
    padding: 1rem 0;
  }
  p {
    padding: 1rem 0;
  }
  .img-container {
    width: 100%;
  }
  .overview {
    text-align: justify;
  }
  .txt-container h1 {
    text-align: center;
  }
  img {
    width: 100%;
    border-radius: 1rem;
  }
  .movie-details {
    margin: 1rem 20%;
  }
  span {
    font-weight: bold;
  }
</style>