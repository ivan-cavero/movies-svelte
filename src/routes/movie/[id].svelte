<script context="module">
	export async function load({ fetch, params }) {
		console.log(params);
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/${params.id}?api_key=${import.meta.env.VITE_API}&language=en-US&page=1`
		);
		const movieDetail = await res.json();
		console.log(movieDetail);
		if (res.ok) {
			return {
				props: { movieDetail }
			};
		} else {
			return {
				error: { status: res.status, message: res.statusText }
			};
		}
	}
</script>

<script>
	import { fly } from 'svelte/transition';

	export let movieDetail;
</script>

<div class="movie-details" in:fly={{y: 50, duration: 500, delay: 500}} out:fly={{duration:500}}>
	<div class="img-container">
		<img
			src={'https://image.tmdb.org/t/p/original' + movieDetail.backdrop_path}
			alt={movieDetail.title}
		/>
	</div>
	<div class="txt-container">
		<h3>{movieDetail.title}</h3>
		<p class="overview">{movieDetail.overview}</p>
		<p>
			<span>Release date:</span>
			{movieDetail.release_date} <br />
			<span>Budget: </span>
			{movieDetail.budget} <br />
			<span>Rating: </span>
			{movieDetail.vote_average} <br />
			<span>Runtime: </span>
			{movieDetail.runtime} mins
		</p>
	</div>
</div>

<style>
	p {
		padding: 1rem 0rem;
	}
	.img-container {
		width: 100%;
		border-radius: 1rem;
	}
	img {
		width: 100%;
		border-radius: 1rem;
	}
	.txt-container {
		padding: 1rem;
	}
	.movie-details {
		margin: 2rem 15%;
		/* make shadow */
		box-shadow: 0 0.5rem 1rem rgba(0, 0, 0, 0.3);
		border-radius: 1rem;
	}
	span {
		font-weight: bold;
	}

	@media (min-width: 400px) {
		.movie-details {
			margin: 2rem 2%;
		}
	}
</style>
