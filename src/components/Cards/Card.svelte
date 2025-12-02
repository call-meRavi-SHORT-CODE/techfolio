<script>
	import { marked } from 'marked';
	import Button from '../Buttons/Button.svelte';

export let title,
	description,
	links,
	image,
	location,
	duration,
	designation,
	onHover,
	defaultAsset,
	compact = false;

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
	class="group border border-gray-200 dark:border-neutral-700 rounded-lg bg-white dark:bg-zinc-900 cursor-default overflow-hidden card-hover shadow-sm hover:shadow-md transition-all duration-300"
	role="button"
	on:mouseenter={handleHover}
	on:mouseleave={handleMouseLeave}
	tabindex="0"
>
	<div class={`flex md:flex-row flex-col ${compact ? 'p-3 md:p-4 gap-3 md:gap-4' : 'p-4 md:p-5 gap-4 md:gap-5'}`}>
		<div class={`md:w-1/4 flex-shrink-0 ${compact ? 'max-w-[90px] md:max-w-[110px]' : 'max-w-[120px] md:max-w-[140px]'}`}>
			<div class="rounded-lg overflow-hidden bg-gray-50 dark:bg-zinc-800 transition-transform duration-300 group-hover:scale-105">
				<img src={img_url} alt="card image" class="w-full h-full object-cover" />
			</div>
		</div>
		<div class="md:w-3/4 flex flex-col gap-2">
			<div class="flex flex-col md:flex-row justify-between gap-2 md:gap-0">
				<div class="flex flex-col gap-1">
					<h3 class="font-semibold text-lg md:text-xl text-gray-900 dark:text-white transition-colors">
						{values.title}
					</h3>
					{#if values.designation}
						<p class="text-sm md:text-base text-gray-600 dark:text-gray-400">{values.designation}</p>
					{/if}
				</div>
				<div class="flex flex-col items-start md:items-end gap-0.5">
					{#if values.duration}
						<span class="text-xs md:text-sm font-semibold text-gray-700 dark:text-gray-300">{values.duration}</span>
					{/if}
					{#if values.location}
						<span class="text-xs md:text-sm text-gray-600 dark:text-gray-400">{values.location}</span>
					{/if}
				</div>
			</div>
			<ul class="list-disc space-y-1.5 ml-4 md:ml-5 text-gray-700 dark:text-gray-300 text-sm md:text-[0.95rem]">
				{#each values.description as desc}
					<li class="leading-relaxed">{@html marked(desc)}</li>
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
