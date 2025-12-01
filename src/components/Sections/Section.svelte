<script>
	import ShowButton from '../Buttons/ShowButton.svelte';
	import { slide } from 'svelte/transition';
	import { onMount } from 'svelte';
	import Card from '../Cards/Card.svelte';

	export let sectionData, defaultAsset;
	const { title, data: items } = sectionData;

	// tag filtering disabled for a simpler, cleaner layout
	export let displayTags = false;
	export let showAll = true;
	export let maxDisplay = 3;
	export let addAllTag = false;

	// remove All / Machine Learning tabs; always show all items
	let tags = [];
	let selectedTag = null;

	const toggleShowAll = () => {
		showAll = !showAll;
	};

	onMount(() => {
		showAll = true;
		displayTags = false;
	});
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

		<!-- tags removed -->
	</div>
	<div class="border-t-2 border-blue-500 dark:border-blue-400 w-24 mt-6 mb-8"></div>
	{#each items as item}
		<div transition:slide={{ duration: 400 }} class="w-full mt-5">
			<Card {...item} {defaultAsset} />
		</div>
	{/each}
</div>
