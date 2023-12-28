<script>
	import { Subhead, H1, Headline, Button } from 'attractions'
	import { configStore } from '/stores/configCopyStore'
	import Typewriter from '../components/Typewriter/Typewriter.svelte'
	import Icon from '@iconify/svelte';

	let name
	let headline
	configStore.subscribe((data) => {
		;(name = data.name), (headline = data.headline)
	})
</script>

<section class="hero">
	<H1>Hey, I'm</H1>
	<Typewriter interval={100} cursor="$main">
		<!--Name-->
		<Headline style="text-overflow: ellipsis;">{name}</Headline>
	</Typewriter>
	<!--Headline-->
	<Subhead>
		{headline}
	</Subhead>
	<br />
	<br />
	<Button
		class="scroll-down"
		round
		filled
		on:click={() => router.push('#summary')}
	>
		<a href="#summary" class="button">
			<Icon icon="tabler:arrow-down" width="24" class="down-icon" />
		</a>
	</Button>

	<br />
</section>

<style lang="scss">
	@use 'theme.scss';
	.hero {
		display: flex;
		flex-direction: column;
		align-items: center;
		:global(.headline) {
			font-size: 5em;
			font-family: theme.$font;
		}
	}
	section {
		text-align: center;
		height: 100vh;
	}
	:global(.scroll-down, .down-icon) {
		margin-inline: auto;
		color: theme.$background;
	}
	:global(.hero.btn:not(#summary)) {
		margin-inline: 500px !important;
	}
</style>
