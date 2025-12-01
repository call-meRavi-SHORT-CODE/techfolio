<script>
	import SvelteMarkdown from 'svelte-exmarkdown';
	import Button from '../Buttons/Button.svelte';
	export let data;

	const { description, links } = data?.about || {};
</script>

<div class="flex flex-col slide-up">
	<h1 class="text-4xl md:text-5xl font-bold text-gray-900 dark:text-white">About Me</h1>
	<div class="border-t-2 border-blue-500 dark:border-blue-400 w-24 mt-4 mb-6"></div>

	<div class="space-y-5">
		{#if description}
			{#each description as desc}
				<p class="text-lg leading-relaxed text-gray-700 dark:text-gray-300">
					<SvelteMarkdown md={desc} />
				</p>
			{/each}
		{/if}
		{#if links}
			<div class="flex flex-wrap gap-4 mt-8">
				{#each links as link}
					<Button {...link} />
				{/each}
			</div>
		{/if}
	</div>
</div>
