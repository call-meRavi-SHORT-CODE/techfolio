<script>
	import Markdown from 'svelte-exmarkdown';
	import Toggle from './Buttons/Toggle.svelte';
	import Icon from '@iconify/svelte';

	export let data, darkMode;

	const githubLink = 'https://github.com/arulkumarann/academic-portfolio';
</script>

<footer
	class="bg-gray-50 dark:bg-zinc-900 border-t border-gray-200 dark:border-neutral-700 py-8 px-6 mt-20"
>
	<div class="container mx-auto max-w-7xl">
		<div class="flex flex-col md:flex-row items-center justify-between gap-6">
			<div class="text-gray-600 dark:text-gray-400 text-sm md:text-base">
				<Markdown md={data} />
			</div>
			<div class="flex flex-row items-center gap-4">
				<a
					href={githubLink}
					class="text-gray-600 dark:text-gray-400 hover:text-blue-600 dark:hover:text-blue-400 transition-all duration-300 hover:scale-110"
					target="_blank"
					rel="noopener noreferrer"
					aria-label="GitHub"
				>
					<Icon icon="akar-icons:github-fill" class="text-2xl" />
				</a>
				{#if darkMode}
					<Toggle />
				{/if}
			</div>
		</div>
	</div>
</footer>
