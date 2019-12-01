<ul class="post-list">
    {#each posts as post}
        <li>
            <a rel='prefetch' href='articles/{getCategorySlug(post)}/{post.slug}'>
                {post.title.rendered}
            </a>
        </li>
    {/each}
</ul>

<ul class="pagination">
    {#each pages as page}
        <li>
            <a href='page/{page}' class="{ page === currentPage ? 'active' : '' }">
                {page}
            </a>
        </li>
    {/each}
</ul>

<script>
    export let posts
    export let pages
    export let currentPage

    function getCategorySlug(post) {
        return post._embedded["wp:term"][0][0].slug
    }


    /*import { onMount } from 'svelte'

    import { stores } from '@sapper/app';
    const { page } = stores();

    let posts = []
    let totalPages = null
    let currentPage = 1
    let pages = []
    let catID = null

    $: if (process.browser && $page.path !== '/') {
        getCategoryID($page.params.slug)
        console.log(catID)
    }



    const apiUrl = process.env.SAPPER_APP_API_URL

    function getCategoryID(slug) {
        fetch(`${apiUrl}/wp/v2/categories?slug=${slug}`).then(res => {
            return res.json()
        }).then(result => {
            catID = result[0].id
            getCategoryPosts()
        })
    }

    function getCategoryPosts() {
        fetch(`${apiUrl}/wp/v2/posts?per_page=2&categories=${catID}`).then(res => {
            totalPages = res.headers.get('X-WP-TotalPages')
            pages = createPagesArray(totalPages)
            return res.json()
        }).then(result => {
            posts = result
            currentPage = 1
        })
    }

    function createPagesArray(total) {
        let arr = []

        for(let i = 1; i <= total; i++) {
            arr.push(i)
        }

        return arr
    }

    function changePage(page) {
        fetch(catID !== null ? `${apiUrl}/wp/v2/posts?per_page=2&categories=${catID}&page=${page}` : `${apiUrl}/wp/v2/posts?per_page=5&page=${page}`).then(res => {
            return res.json()
        }).then(result => {
            posts = result
            currentPage = page
        })
    }

    onMount(async () => {
        const res = await fetch(`${apiUrl}/wp/v2/posts?per_page=5&_embed`)
        posts = await res.json()

        totalPages = res.headers.get('X-WP-TotalPages')

        pages = createPagesArray(totalPages)

        console.log(pages);
    })*/
</script>

<style lang="scss">
    .pagination,
    .post-list {
        margin: 0;
        padding: 0;
        list-style: none;
    }

    .pagination {
        display: flex;
        margin-top: 40px;

        li {
            margin-right: 10px;

            &:last-of-type {
                margin-right: 0;
            }
        }

        a {
            display: inline-block;
            padding: 10px 15px;
            border: 1px solid #cccccc;
            cursor: pointer;

            &.active {
                cursor: default;
                background: #FF3E00;
                color: #ffffff;
            }
        }
    }


</style>


