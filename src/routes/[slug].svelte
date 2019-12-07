<script context="module">
    const apiUrl = process.env.SAPPER_APP_API_URL

    export async function preload({ params, query }) {
        const res = await this.fetch(`${apiUrl}/wp/v2/pages?slug=${params.slug}`)
        const data = await res.json()


        return { page: data[0] }
    }
</script>

<script>
    export let page
</script>

<h1>{page.title.rendered}</h1>

<div class="content">
    {@html page.content.rendered}
</div>

