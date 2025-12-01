<script>
	import Icon from '@iconify/svelte';
	export let data, defaultAsset;

	const img_url = `/images/${data?.image || defaultAsset}`;
	const { sidebar } = data;
</script>

<aside
	class="md:w-1/5 w-full md:sticky md:top-20 md:h-[calc(100vh-5rem)] p-8 hidden md:block"
>
	<div class="flex flex-col items-start space-y-6 fade-in">
		<div class="w-full flex justify-center mb-4">
			<div class="relative group">
				<div class="absolute -inset-1 bg-gradient-to-r from-blue-600 to-blue-400 rounded-full opacity-25 group-hover:opacity-40 blur transition duration-500"></div>
				<img src={img_url} alt={data?.name} class="relative w-48 h-48 rounded-full object-cover ring-4 ring-white dark:ring-zinc-900 shadow-xl" />
			</div>
		</div>

		<div class="w-full">
			<h1 class="text-2xl font-bold text-gray-900 dark:text-white">{data?.name}</h1>

			{#if sidebar?.description}
				<p class="text-base text-gray-600 dark:text-gray-400 mt-3 leading-relaxed">{sidebar?.description}</p>
			{/if}

			{#if sidebar?.details}
				<div class="space-y-3 mt-6">
					{#each sidebar.details as item}
						<div class="flex items-center gap-3 text-gray-700 dark:text-gray-300">
							<Icon icon={item.icon} class="text-xl text-blue-600 dark:text-blue-400 flex-shrink-0" />
							<span class="text-sm">{item.text}</span>
						</div>
					{/each}
				</div>
			{/if}
		</div>
	</div>
</aside>
