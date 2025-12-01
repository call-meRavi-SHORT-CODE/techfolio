<script>
	export let NavData, defaultAsset;
	const { title, links, icon, separator } = NavData;

	const img_url = `/images/${icon || defaultAsset}`;
</script>

<nav
	class="sticky top-0 bg-white/80 dark:bg-zinc-900/80 backdrop-blur-lg border-b border-gray-200 dark:border-neutral-700 z-50 transition-all duration-300"
>
	<div class="container mx-auto max-w-7xl px-6 py-4">
		<div class="flex justify-between items-center gap-10">
			<div class="flex items-center gap-4">
				{#if icon}
					<div class="w-12 h-12 rounded-full overflow-hidden ring-2 ring-blue-500/20 dark:ring-blue-400/20 transition-transform duration-300 hover:scale-110">
						<img src={img_url} alt="logo" class="w-full h-full object-cover" />
					</div>
				{/if}
				<a class="text-gray-800 dark:text-gray-200 text-xl font-bold link-hover-border transition-colors" href="/">{title}</a>
			</div>
			<div class="hidden md:flex gap-6 items-center">
				{#each links as { title, url }, index}
					<a
						class="text-gray-600 dark:text-gray-300 text-base font-medium link-hover-border hover:text-blue-600 dark:hover:text-blue-400 transition-colors"
						target="_blank"
						rel="noopener noreferrer"
						href={url}>{title}</a
					>
					{#if separator && index !== links.length - 1}
						<span class="text-gray-400 dark:text-gray-600">{separator}</span>
					{/if}
				{/each}
			</div>
		</div>
	</div>
</nav>
