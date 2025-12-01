<script>
	import Markdown from 'svelte-exmarkdown';
	import Button from '../Buttons/Button.svelte';

	export let title,
		description,
		links,
		image,
		location,
		duration,
		designation,
		onHover,
		defaultAsset;

	let img_url = `/images/${image ?? defaultAsset}`;

	let values = { title, description, links, image, location, duration, designation };
	let originalValues = {};

	function storeOriginalValues() {
		originalValues = { ...values };
	}

	function handleHover() {
		if (onHover) {
			const { image: hoverImage, ...hoverProps } = onHover[0];
			img_url = `/images/${hoverImage ?? image ?? defaultAsset}`;
			Object.keys(hoverProps).forEach((prop) => {
				if (prop in originalValues) {
					values[prop] = hoverProps[prop];
				}
			});
		}
	}

	function handleMouseLeave() {
		img_url = `/images/${image ?? defaultAsset}`;
		values = { ...originalValues };
	}

	$: storeOriginalValues();
</script>

<div
	class="group border border-gray-200 dark:border-neutral-700 rounded-xl bg-white dark:bg-zinc-900 cursor-default overflow-hidden card-hover shadow-sm hover:shadow-lg transition-all duration-300"
	role="button"
	on:mouseenter={handleHover}
	on:mouseleave={handleMouseLeave}
	tabindex="0"
>
	<div class="flex md:flex-row flex-col p-6 gap-6">
		<div class="md:w-1/4 flex-shrink-0">
			<div class="rounded-xl overflow-hidden bg-gray-50 dark:bg-zinc-800 transition-transform duration-300 group-hover:scale-105">
				<img src={img_url} alt="Experience Logo" class="w-full h-full object-cover" />
			</div>
		</div>
		<div class="md:w-3/4 flex flex-col gap-3">
			<div class="flex flex-col md:flex-row justify-between gap-3 md:gap-0">
				<div class="flex flex-col gap-1">
					<h3 class="font-bold text-xl text-gray-900 dark:text-white transition-colors">{values.title}</h3>
					<p class="text-base text-gray-600 dark:text-gray-400">{values.designation}</p>
				</div>
				<div class="flex flex-col items-start md:items-end gap-1">
					<span class="text-sm font-semibold text-gray-700 dark:text-gray-300">{values.duration}</span>
					<span class="text-sm text-gray-600 dark:text-gray-400">{values.location}</span>
				</div>
			</div>
			<ul class="list-disc space-y-2 ml-5 text-gray-700 dark:text-gray-300">
				{#each values.description as desc}
					<li class="leading-relaxed"><Markdown md={desc} /></li>
				{/each}
			</ul>
			{#if values.links}
				<div class="flex flex-wrap gap-3 mt-2">
					{#each values.links as link}
						<Button {...link} />
					{/each}
				</div>
			{/if}
		</div>
	</div>
</div>
