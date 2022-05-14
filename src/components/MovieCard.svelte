<script>
	export let movie;
</script>

<div class="movie-card">
	<a sveltekit:prefetch sveltekit:noscroll href={'/movie/' + movie.id}>
		<img src={'https://image.tmdb.org/t/p/w500' + movie.poster_path} alt={movie.title} />
	</a>
	<div class="description">
		<h3>{movie.title}</h3>
		<time time={movie.release_date}>{movie.release_date}</time>
	</div>
</div>

<style>
	img {
		width: 100%;
		height: 30vh;
		border-radius: 1rem;
	}
	.description {
		padding: 1rem;
	}
	.movie-card {
		display: flex;
		flex-direction: column;
		align-items: center;
		/* make shadow */
		box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.3);
		border-radius: 1rem;
	}
</style>
