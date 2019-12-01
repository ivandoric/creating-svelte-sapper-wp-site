<script context="module">
	const apiUrl = process.env.SAPPER_APP_API_URL

	export async function preload({ params, query }) {
		const res = await this.fetch(`${apiUrl}/wp/v2/categories`)
		const categories = await res.json()

		return {
			categories
		}
	}
</script>

<script>
	import Nav from '../components/Nav.svelte';
	import CategoryList from '../components/CategoryList.svelte'

	export let segment;
	export let categories
</script>

<style>
	main {
		display: flex;
		position: relative;
		max-width: 56em;
		background-color: white;
		padding: 2em;
		margin: 0 auto;
		box-sizing: border-box;
	}
</style>

<Nav {segment}/>

<main>
	<CategoryList categories={categories} />

	<div class="content">
		<slot></slot>
	</div>
</main>
