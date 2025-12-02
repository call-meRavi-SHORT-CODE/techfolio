<script>
	export let data;

	import About from '../components/Sections/About.svelte';
	import Section from '../components/Sections/Section.svelte';

	import Nav from '../components/Nav.svelte';
	import Sidebar from '../components/Sidebar.svelte';
	import MobileSidebar from '../components/MobileSidebar.svelte';
	import Footer from '../components/Footer.svelte';

	const { info, sections, config } = data;
	const { navbar: NavData, footer: FooterData } = info;
	const { darkMode, maxDisplay, addAllTag, defaultAsset } = config;
</script>

<div class="min-h-screen bg-gradient-to-br from-gray-50 to-white dark:from-zinc-950 dark:to-zinc-900 transition-colors duration-300">
	{#if NavData}
		<Nav {NavData} {defaultAsset} socials={info.socials} />
	{/if}
	<div class="flex flex-col md:flex-row max-w-7xl mx-auto">
		<Sidebar data={info} {defaultAsset} />
		{#if NavData}
			<MobileSidebar data={info} {defaultAsset} />
		{/if}
		<main class="md:w-4/5 w-full px-6 md:px-12 py-12 md:py-16">
			<div class="max-w-5xl mx-auto space-y-16">
				{#if info}
					<About data={info} />
				{/if}
				{#each sections as sectionData}
					<Section
						{sectionData}
						{maxDisplay}
						addAllTag={sectionData.addAllTag ?? addAllTag}
						{defaultAsset}
					/>
				{/each}
			</div>
		</main>
	</div>
	{#if FooterData}
		<Footer data={FooterData} {darkMode} socials={info.socials} />
	{/if}
</div>
