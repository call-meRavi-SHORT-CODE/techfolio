<script>
	import Icon from '@iconify/svelte';

	export let text, link, firstUpperCase, icon, iconOnly, buttonIcon;

	text = firstUpperCase ? text.charAt(0).toUpperCase() + text.slice(1) : text;
</script>

{#if iconOnly}
	<a href={link} target="_blank" rel="noopener noreferrer" class="transition-transform duration-200 hover:scale-110">
		<Icon {icon} />
	</a>
{:else}
	<a
		href={link}
		class="group relative inline-flex items-center justify-center gap-2 px-5 py-2.5 text-base font-semibold text-blue-700 bg-blue-50 dark:bg-blue-900/20 dark:text-blue-400 rounded-lg overflow-hidden transition-all duration-300 hover:bg-blue-100 dark:hover:bg-blue-900/30 hover:shadow-md hover:-translate-y-0.5 active:translate-y-0"
		target="_blank"
		rel="noopener noreferrer"
	>
		<span class="absolute inset-0 bg-gradient-to-r from-blue-600/0 via-blue-600/5 to-blue-600/0 translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-700"></span>
		{#if icon || buttonIcon}
			<Icon {icon} class="text-xl transition-transform duration-300 group-hover:scale-110" />
		{/if}
		{#if text && !iconOnly}
			<span class="relative">{text}</span>
		{/if}
	</a>
{/if}
