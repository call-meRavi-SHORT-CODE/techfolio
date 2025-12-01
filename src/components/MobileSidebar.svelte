<script>
	export let data, defaultAsset;
	const { sidebar } = data;

	const img_url = `/images/${data?.image || defaultAsset}`;
</script>

<aside
	class="w-full flex md:hidden gap-4 p-4 bg-white dark:bg-zinc-900 border-b border-gray-200 dark:border-neutral-700"
>
	<div class="flex-shrink-0">
		<div class="w-16 h-16 rounded-full overflow-hidden ring-2 ring-blue-500/20 dark:ring-blue-400/20">
			<img src={img_url} alt={data?.name} class="w-full h-full object-cover" />
		</div>
	</div>
	<div class="flex flex-col justify-center">
		<h1 class="text-xl font-bold text-gray-900 dark:text-white">{data?.name}</h1>
		{#if sidebar?.description}
			<p class="text-sm text-gray-600 dark:text-gray-400 mt-1">{sidebar?.description}</p>
		{/if}
	</div>
</aside>
