<script>
    import { onMount } from 'svelte'

    let posts = []

    const apiUrl = process.env.SAPPER_APP_API_URL

    onMount(async () => {
        const res = await fetch(`${apiUrl}/wp/v2/posts`)
        const json = await res.json()
        posts = json
        console.log(posts)
    })
</script>

<ul>
    {#each posts as post}
        <li>
            <a rel='prefetch' href='articles/{post.slug}'>
                {post.title.rendered}
            </a>
        </li>
    {/each}
</ul>
