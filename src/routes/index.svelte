<svelte:head>
	<title>Sapper WordPress Site</title>
</svelte:head>

<script>
	import PostsList from '../components/PostsList.svelte'
	import CategoryList from '../components/CategoryList.svelte'
</script>


<div class="cats-posts">
	<CategoryList />

	<div class="posts">
		<PostsList />
	</div>
</div>

<style lang="scss">
	.cats-posts {
		display: flex;
	}
</style>




