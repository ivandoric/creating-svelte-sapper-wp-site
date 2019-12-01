<svelte:head>
	<title>Sapper WordPress Site</title>
</svelte:head>

<script context="module">
	const apiUrl = process.env.SAPPER_APP_API_URL

	function createPagesArray(total) {
		let arr = []

		for(let i = 1; i <= total; i++) {
			arr.push(i)
		}

		return arr
	}

	export async function preload({ params, query }) {
		const res = await this.fetch(`${apiUrl}/wp/v2/posts?per_page=5&_embed`)
		const posts = await res.json()
		const totalPages = res.headers.get('X-WP-TotalPages')

		const pages = createPagesArray(totalPages)

		return {
			posts,
			pages,
			currentPage: 1
		}
	}
</script>

<script>
	import PostsList from '../components/PostsList.svelte'

	export let posts
	export let pages
	export let currentPage
</script>


<PostsList posts={posts} pages={pages} currentPage={currentPage}/>





