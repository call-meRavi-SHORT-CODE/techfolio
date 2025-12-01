<script>
	import ShowButton from '../Buttons/ShowButton.svelte';
	import { slide } from 'svelte/transition';
	import { onMount } from 'svelte';
	import Card from '../Cards/Card.svelte';

	export let sectionData, defaultAsset;
	const { title, data: items } = sectionData;

	export let displayTags = false;
	export let showAll = false;
	export let maxDisplay = 3;
	export let addAllTag = false;

	if (addAllTag) {
		items.forEach((item) => {
			item.tags = ['All', ...new Set(item.tags)];
		});
	}

	let tags = [...new Set(items.flatMap((item) => item.tags))];
	let selectedTag = tags[0];

	const toggleShowAll = () => {
		showAll = !showAll;
	};

	onMount(() => {
		if (items.length <= maxDisplay) {
			showAll = true;
		}
	});

	displayTags = tags.length > 1 || displayTags;
</script>

<div class="flex flex-col items-center mt-20 md:mt-28 slide-up" id={title?.toLowerCase()}>
	<div class="flex flex-col md:flex-row justify-between w-full items-start md:items-center gap-4 md:gap-0">
		<a
			class="group text-4xl md:text-5xl font-bold text-gray-900 dark:text-white hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-300"
			href={`#${title?.toLowerCase()}`}
		>
			<span>{title}</span>
			<span
				class="text-3xl font-bold text-blue-600 dark:text-blue-400 opacity-0 group-hover:opacity-100 transition-opacity duration-300"
				>#</span
			>
		</a>

		{#if displayTags}
			<div class="flex flex-wrap gap-3 md:gap-4 items-center">
				{#each tags as tag}
					<button
						class={`px-4 py-2 rounded-lg text-sm font-medium transition-all duration-300 ${
							selectedTag === tag
								? 'bg-blue-100 dark:bg-blue-900/30 text-blue-700 dark:text-blue-400 shadow-sm'
								: 'text-gray-600 dark:text-gray-400 hover:bg-gray-100 dark:hover:bg-zinc-800'
						}`}
						on:click={() => (selectedTag = tag)}
					>
						{tag}
					</button>
				{/each}
			</div>
		{/if}
	</div>
	<div class="border-t-2 border-blue-500 dark:border-blue-400 w-24 mt-6 mb-8"></div>
	{#each items as item, index}
		{#if item?.tags?.includes(selectedTag) && (showAll || index < maxDisplay)}
			<div transition:slide={{ duration: 400 }} class="w-full mt-5">
				<Card {...item} {defaultAsset} />
			</div>
		{/if}
	{/each}

	{#if items.filter((item) => item.tags.includes(selectedTag)).length > maxDisplay}
		<ShowButton onClick={toggleShowAll} text={showAll ? 'Show less' : 'Show more'} />
	{/if}
</div>
