<script>
	import { marked } from 'marked';
	import Toggle from './Buttons/Toggle.svelte';
	import Icon from '@iconify/svelte';
	import Button from './Buttons/Button.svelte';

	export let data, darkMode, socials = {};

	const socialEntries = Object.entries(socials || {});
</script>

<footer
	class="bg-gray-50 dark:bg-zinc-900 border-t border-gray-200 dark:border-neutral-700 py-8 px-6 mt-20"
>
	<div class="container mx-auto max-w-7xl">
		<div class="flex flex-col md:flex-row items-center justify-between gap-6">
			<div class="text-gray-600 dark:text-gray-400 text-sm md:text-base">
				{@html marked(data)}
			</div>
			<div class="flex flex-row items-center gap-4">
				{#if socialEntries.length}
					<ul class="flex items-center gap-3 md:gap-4">
						{#each socialEntries as [key, value]}
							<li class="tooltip-wrapper">
								<Button
									text={key}
									link={value?.link}
									icon={value?.icon}
									iconOnly={true}
								/>
							</li>
						{/each}
					</ul>
				{/if}
				{#if darkMode}
					<Toggle />
				{/if}
			</div>
		</div>
	</div>
</footer>
