<ul class="cats post-list">
    {#each categories as category}
        <li><a href='categories/{category.slug}'>{category.name}</a></li>
    {/each}
</ul>

<script>
    import { onMount } from 'svelte'

    let categories = []

    const apiUrl = process.env.SAPPER_APP_API_URL

    onMount(async () => {
        const res = await fetch(`${apiUrl}/wp/v2/categories?per_page=100`)
        categories = await res.json()
    })
</script>

<style lang="scss">
    .cats {
        margin-top: 0;
        margin-right: 20px;
        padding: 20px;
        background: #efefef;
        list-style: none;
    }
</style>
