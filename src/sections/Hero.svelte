<script>
	import { Subhead, H1, Headline, Button } from 'attractions'
	import { configStore } from '/stores/configCopyStore'
	import Typewriter from '../components/Typewriter/Typewriter.svelte'
	import { ArrowDownIcon } from 'svelte-feather-icons'

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
		<Headline>{name}</Headline>
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
			<ArrowDownIcon size="24" class="down-icon" />
		</a>
	</Button>

	<br />
</section>

<style lang="scss">
	@use 'theme.scss';
	.hero {
		display: flex;
		flex-direction: column;
		:global(.headline) {
			font-size: 100px;
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
