<ul class="cats post-list">
    {#each categories as category}
        <li><a href='categories/{category.slug}'>{category.name}</a></li>
    {/each}
</ul>

<script>
    export let categories
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
