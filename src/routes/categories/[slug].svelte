<svelte:head>
    <title>Categories</title>
</svelte:head>

<script>
    import PostsList from '../../components/PostsList.svelte'
    import CategoryList from '../../components/CategoryList.svelte'
</script>

<h1>This is a category page</h1>

<div class="cats-posts">
    <CategoryList />

    <div class="posts">
        <PostsList  />
    </div>
</div>

<style lang="scss">
    .cats-posts {
        display: flex;
    }
</style>
