<script>
	export let onClick;
	export let text;
</script>

<div class="border-t border-gray-200 dark:border-neutral-700 w-full mt-6"></div>

<button
	class="group relative w-48 md:w-96 px-6 py-3 text-base font-semibold text-blue-700 dark:text-blue-400 bg-blue-50 dark:bg-blue-900/20 hover:bg-blue-100 dark:hover:bg-blue-900/30 rounded-lg transition-all duration-300 hover:shadow-md hover:-translate-y-0.5 active:translate-y-0 overflow-hidden"
	on:click={onClick}
>
	<span class="absolute inset-0 bg-gradient-to-r from-blue-600/0 via-blue-600/5 to-blue-600/0 translate-x-[-100%] group-hover:translate-x-[100%] transition-transform duration-700"></span>
	<span class="relative">{text}</span>
</button>
