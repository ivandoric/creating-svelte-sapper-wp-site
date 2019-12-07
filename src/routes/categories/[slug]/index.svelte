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
        const catResponse = await this.fetch(`${apiUrl}/wp/v2/categories?slug=${params.slug}`)
        const cat = await catResponse.json()
        const catID = cat[0].id
        const catName = cat[0].name

        const res = await this.fetch(`${apiUrl}/wp/v2/posts?per_page=2&_embed&categories=${catID}`)
        const posts = await res.json()
        const totalPages = res.headers.get('X-WP-TotalPages')

        const pages = createPagesArray(totalPages)

        return {
            posts,
            pages,
            catName,
            currentPage: 1,
            isCategoryPage: true,
            catSlug: params.slug
        }
    }
</script>

<script>
    import PostsList from '../../../components/PostsList.svelte'

    export let posts
    export let pages
    export let catName
    export let currentPage
    export let isCategoryPage
    export let catSlug
</script>

<h1>Listing posts from <strong>{catName}</strong> category</h1>

<PostsList posts={posts} pages={pages} currentPage={currentPage} isCategoryPage={isCategoryPage} catSlug={catSlug} />
