<script context="module">
	export async function load({ fetch }) {
		const res = await fetch(
			`https://api.themoviedb.org/3/movie/popular?api_key=${import.meta.env.VITE_API}&language=en-US&page=1`
		);
		const data = await res.json();
		console.log(data);
		if (res.ok) {
			return {
				props: { popular: data.results }
			};
		} else {
			return {
				error: { status: res.status, message: res.statusText }
			};
		}
	}
</script>

<script>
	import PopularMovies from '../components/PopularMovies.svelte';
	import SearchMovies from '../components/SearchMovies.svelte';
	import global from '../global.css';
	import { fly } from 'svelte/transition';

	export let popular;
</script>

<section in:fly={{y: 50, duration: 500, delay: 500}} out:fly={{duration:500}}>
	<SearchMovies />
	<PopularMovies {popular} />
</section>
