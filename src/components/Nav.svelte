<nav>
	<ul>
		{#each menuItems.items as item}
			<li>
				<a class:selected='{item.slug === "home" ? segment === undefined : segment === item.slug }'
				   href='{ item.slug === "home" ? "." : item.slug  }'>
					{item.title}
				</a>

				{#if item.child_items !== undefined}
					<ul class="subitems">
						{#each item.child_items as subitem }
							<li>
								<a class:selected='{segment === subitem.url }' href='{ subitem.url  }'>
									{subitem.title}
								</a>
							</li>
						{/each}
					</ul>
				{/if}
			</li>
		{/each}
	</ul>
</nav>

<script>
	export let segment
	export let menuItems
</script>

<style lang="scss">
	nav {
		border-bottom: 1px solid rgba(255,62,0,0.1);
		font-weight: 300;
		padding: 0 1em;
	}

	ul {
		margin: 0;
		padding: 0;

		ul.subitems {
			display: none;
			position: absolute;
			top: 100%;
			left: 0;
			border: 1px solid #efefef;
			min-width: 200px;

			li {
				float: none;

				&:hover {
					background: #efefef;
				}
			}
		}
	}

	/* clearfix */
	ul::after {
		content: '';
		display: block;
		clear: both;
	}

	li {
		display: block;
		float: left;
		position: relative;

		&:hover .subitems {
			display: block;
		}
	}

	.selected {
		position: relative;
		display: inline-block;
	}

	.selected::after {
		position: absolute;
		content: '';
		width: calc(100% - 1em);
		height: 2px;
		background-color: rgb(255,62,0);
		display: block;
		bottom: -1px;
	}

	a {
		text-decoration: none;
		padding: 1em 0.5em;
		display: block;
	}
</style>
