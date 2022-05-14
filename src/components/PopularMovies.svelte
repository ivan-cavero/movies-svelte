<script>
	import MovieCard from './MovieCard.svelte'
	
	export let popular;
	console.log(popular[1]);
</script>

<h1>Popular Movies</h1>
<div>
	{#each popular as movie}
		<MovieCard {movie} />
	{/each}
</div>

<style>
	h1 {
		text-align: center;
		margin-bottom: 2rem;
	}
	div {
		display: grid;
		grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
		grid-gap: 1rem;
	}
</style>
