<script>
	import { Divider } from 'attractions'
	// Sections

	// import Skills from '../sections/Skills.svelte'
	import Summary from '../sections/Summary.svelte'
	import RecentProjects from '../sections/RecentProjects.svelte'
	import Hero from '../sections/Hero.svelte'
</script>

<container>
	<Hero />
	<br id="summary">
	<br>
	<br>
	<br>
	<br>
	<br>
	<br>
	<div>
		<Summary />
	</div>
	<section class="row">
		<RecentProjects />
		
		<!-- <Skills /> -->
	</section>
</container>

<style>
	section {
		display: flex;
		justify-content: space-around;
		width: 100%;
	}
</style>
