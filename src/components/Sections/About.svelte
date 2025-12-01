<script>
	import Button from '../Buttons/Button.svelte';
	export let data;

	const name = data?.name ?? 'Arul';
	const headline = "AI Engineer with a passion for building AI Agents.";
	const subheadline = 'Specialized in Computer Vision and Natural Language Processing.';
	const { links } = data?.about || {};
</script>

<section class="slide-up">
	<div class="space-y-6 md:space-y-8">
		<h1 class="text-4xl md:text-6xl font-extrabold tracking-tight text-gray-900 dark:text-white">
			Hi, I'm {name.split(' ')[0]}
		</h1>
		<div class="max-w-3xl space-y-3 md:space-y-4">
			<p class="text-lg md:text-2xl font-medium text-gray-800 dark:text-gray-100">
				{headline}
			</p>
			<p class="text-base md:text-lg text-gray-600 dark:text-gray-300">
				{subheadline}
			</p>
		</div>

		{#if links}
			<div class="flex flex-wrap gap-4 pt-2">
				{#each links as link}
					<Button {...link} />
				{/each}
			</div>
		{/if}
	</div>
</section>
