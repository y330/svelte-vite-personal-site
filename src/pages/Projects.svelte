<script>
	// Components
	import Typewriter from './../components/Typewriter/Typewriter.svelte'
	import { Headline } from 'attractions'
	import ResponsiveGrid from './../components/ResponsiveGrid.svelte'
	import Project from './../components/Project.svelte'

	import { configStore } from '/stores/configCopyStore'
	let projects
	configStore.subscribe((data) => {
		projects = data.projects
	})
</script>

<div class="title">
	<Typewriter interval={100} cursor="#ff3e00">
		<Headline>Projects</Headline>
	</Typewriter>
</div>
<section>
	<ResponsiveGrid>
		{#each projects as project}
			<Project
				project={{
					title: project.title,
					description: project.description,
					tech: project.tech,
					url: project.url,
					imageUrl: project.imageUrl,
					videoUrl: project.videoUrl,
					code: project.code,
				}}
				class="module"
			/>
		{/each}
	</ResponsiveGrid>
</section>

<style>
	.title {
		/* padding-top1: 8rem; */
	}
</style>
