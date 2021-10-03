<script>
	// ------- imports
	import { onMount } from 'svelte'
	import { fade, slide } from 'svelte/transition'
	import { tweened } from 'svelte/motion'
	import { cubicOut } from 'svelte/easing'
	import Chips from './Chips.svelte'
	import Typewriter from './Typewriter/Typewriter.svelte'
	import { H2, Label } from 'attractions'
	// ------- parameters
	export let project = {
		title: '',
		description: '',
		tech: [],
		url: '#',
		imageUrl: '#',
		code: '',
	}
	// -------- state
	let hovered = false
	// -------- code
	const shadow = tweened(0, { duration: 500, easing: cubicOut })
	const handleClick = () => {
		// window.location = project.url
	}
	const handleMouseEnter = () => {
		shadow.set(1)
		hovered = true
	}
	const handleMouseLeave = () => {
		shadow.set(0)
		hovered = false
	}
	const randomInt = (min, max) => {
		min = Math.ceil(min)
		max = Math.floor(max)
		return Math.floor(Math.random() * (max - min) + min) //The maximum is exclusive and the minimum is inclusive
	}

	let mounted = false
	
	onMount(() => (mounted = true))
</script>

{#if mounted}
	<div
		on:click={handleClick}
		on:mouseenter={handleMouseEnter}
		on:touchstart={handleMouseEnter}
		on:mouseleave={handleMouseLeave}
		on:touchend={handleMouseLeave}
		transition:slide={{ delay: randomInt(200, 500) }}
		style="box-shadow: {$shadow * 8}px {$shadow * 4}px #ff3e00, {$shadow *
			16}px {$shadow * 8}px rgba(255, 85, 0, 0.55), {$shadow *
			24}px {$shadow * 12}px rgba(255, 100, 0.6, 0.22);
;"
		class="site dark-mode scroll__ card"
	>
		<container class="site__header">
			<H2 class="title"
				><a class="h2" href={project.url}>
					<Typewriter interval={100}>
						{project.title}
					</Typewriter>
				</a>
			</H2>
		</container>
		<div
			class="description"
			transition:fade={{ delay: randomInt(250, 1000) }}
		>
			{project.description}
		</div>
		<Label
			style="margin-right: 0.1em;text-align: center; border-radius: 2em;padding: 0.2em; background-color: #ff3e00; color: #fff"
			>Interactive demo:</Label
		>
		{#if project.url.includes('github.com') || project.url.includes('chrome.google.com')}
			<img src={project.imageUrl} alt="A screenshot of {project.title}" />
		{:else}
			<iframe src={project.url} frameborder="0" allowfullscreen />
		{/if}
		<br />
		<Label
			style="margin-right: 0.1em;text-align: center; border-radius: 2em;padding: 0.2em; background-color: #ff3e00; color: #fff"
			>Technologies used:</Label
		>
		<div class="technologies">
			<Chips tags={project.tech} />
		</div>
		{#if project.code != ''}Source: <a href={project.code}>{project.code}</a
			>{/if}
	</div>
{/if}

<style lang="scss">
	@use 'theme.scss';

	.site {
		flex: 1 1 250px;
		display: flex;
		flex-direction: column;
		border: 2px theme.$tertiary solid;
		border-radius: 15px;
		margin: 1rem;
		padding: 1rem;
		padding-top: 0;
		padding-right: 0;
		min-width: 150px;
		max-width: 500px;
		max-height: 600px;
		overflow-y: scroll;
		position: relative;
		cursor: pointer;
		justify-content: space-between;
	}
	.site__header {
		position: relative;
		// width: 100%;
		background-color: theme.$main;
		margin-right: 0.5em;
		margin-left: -0.5em;
		text-align: center;
		opacity: 0.8;
		border-radius: 0.2em;
		padding: 0.2em;
	}
	.site {
		&:hover {
			border-color: theme.$main;
			color: var(--accent-color);
			&::-webkit-scrollbar-thumb {
				background-color: theme.$main;
			}
			& .title {
				/* border: 2px white solid; */
				color: white;

				background-color: theme.$secondary;
				a {
					&::after {
						content: ' (click to view project)';
						opacity: 1;
						text-decoration: underline;
					}
				}
			}
			& .description {
				// color: theme.$main;
			}
		}
		.title {
			border-radius: 7px 0px 0 7px;
			/* width: 110%; */
			padding: 0;
			// padding-top: 2em;
			height: 2rem;
			text-align: center;
			position: fixed;
			max-height: 2rem;
			font-weight: 400;
			opacity: 0.6;
			transition-property: opacity, background-color;
			transition-duration: 300ms ease-in-out;
			a {
				color: theme.$background;

				text-decoration: none;
				&::after {
					content: ' (click to view project)';
					min-height: 5rem;
					font-size: small;
					transition-duration: 0.5s;
					text-decoration: none;
					opacity: 0.2;
				}
			}
		}
	}
	.description {
		margin-top: 3rem;
		flex: 1;
		padding: 1rem;
	}
	iframe {
		margin-block: -0.29em;
		margin-inline: 80.5px 80px;
		// max-height: 70%;
		max-width: 250%;
		position: relative;
		height: 1em;
		border: 0.1px solid theme.$secondary;
		align-self: center;
		border-radius: 1px;
		transform: scale(0.4);
		zoom: 40;
		background-color: white;
	}
	img {
		margin-left: 0.1em;
		margin-right: 0.1em;
		margin-top: 0.2em;
		max-height: 70%;
		max-width: 100%;
		/* border-right: 20px solid black; */
		align-self: center;
		border-radius: 10px;
	}
	.code {
		flex: 1;
	}
	.technologies {
		margin-inline: -2.5em;
		// padding-right: 1em;
		display: flex;
		margin-top: -1em;
		justify-content: space-evenly;
		transform: scale(0.75);
	}
</style>
