<script>
    import { onMount } from 'svelte'

    let posts = []

    onMount(async () => {
        const res = await fetch('http://sapperapi.localhost/wp-json/wp/v2/posts')
        const json = await res.json()
        posts = json
        console.log(posts)
    })
</script>

<ul>
    {#each posts as post}
        <li>{post.title.rendered}</li>
    {/each}
</ul>
