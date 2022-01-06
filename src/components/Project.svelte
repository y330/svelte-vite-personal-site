<script>
	// ------- imports
	import { onMount } from 'svelte'
	import { fade, slide } from 'svelte/transition'
	import { tweened } from 'svelte/motion'
	import { cubicOut } from 'svelte/easing'
	// Components
	import Chips from './Chips.svelte'
	import Typewriter from './Typewriter/Typewriter.svelte'
	import Fullscreen from './Fullscreen.svelte'
	import { H2, Label } from 'attractions'
	// ------- parameters
	export let project = {
		title: '',
		description: '',
		tech: [],
		url: '#',
		imageUrl: '#',
		videoUrl: '#',
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
		style="box-shadow: {$shadow * 6}px {$shadow * 3}px #ff3e00, {$shadow *
			10}px {$shadow * 5}px rgba(255, 85, 0, 0.55), {$shadow *
			14}px {$shadow * 7}px rgba(255, 100, 0.6, 0.22);
;"
		class="site dark-mode scroll__ card"
	>
		<container class="site__header">
			<a class="title" href={project.url}>
				<Typewriter interval={20}>
					{project.title}
				</Typewriter>
			</a>
		</container>
		<div
			class="description"
			transition:fade={{ delay: randomInt(250, 1000) }}
		>
			{project.description}
		</div>
		<Label style="margin-top: 1em;" class="project-label"
			>Interactive demo:</Label
		>
		<Fullscreen let:isFull>
			<div>
				{#if project.imageUrl == 'this is a video'}
					<video controls="" autoplay="" name="media"
						><source
							src={project.videoUrl}
							type="video/mp4"
						/></video
					>
				{:else if !isFull}
					<img
						src={project.imageUrl}
						alt="A screenshot of {project.title}"
					/>
				{:else if project.url.includes('github.com') || project.url.includes('chrome.google.com')}
					<img
						src={project.imageUrl}
						alt="A screenshot of {project.title}"
					/>
				{:else}
					<iframe src={project.url} frameborder="0" allowfullscreen />
				{/if}
			</div>
		</Fullscreen>

		<!-- {#if project.url.includes('github.com') || project.url.includes('chrome.google.com')}{:else}

		{/if} -->
		<br />
		<Label class="project-label">Technologies used:</Label>
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
		flex: 1 1 450px;
		display: flex;
		flex-direction: column;
		border: 2px theme.$tertiary solid;
		border-radius: 15px;
		margin: 1rem;
		padding: 1rem;
		padding-top: 0;
		padding-right: 0;
		min-width: 150px;
		max-width: 800px;
		min-height: fit-content;
		overflow-y: scroll;
		position: relative;
		cursor: pointer;
		align-content: flex-end;
		justify-content: space-around;
	}

	.site {
		background-color: rgba(155, 155, 155, 0.1);

		&:hover {
			border-color: theme.$main;
			color: var(--accent-color);
			&::-webkit-scrollbar-thumb {
				background-color: theme.$main;
			}
			h2 {
				background-color: rgba(100, 100, 100, 0.6);
			}
			& .title {
				color: theme.$main;
				&::after {
					content: 'Go to project website';
					opacity: 1;
				}
			}
		}
		.title {
			// top: 0;
			border-radius: 7px 0px 0 7px;
			width: 90%;
			color: theme.$main;
			font-weight: bold;
			font-size: large;
			padding: 0;
			margin-top: 0;
			// height: fit-content;
			text-align: center;
			position: relative;
			// max-height: 8rem;
			transition-property: color, opacity, background-color;
			transition-duration: 300ms ease-in-out;

			text-decoration: none;
			// color: white !important;
			&::after {
				text-decoration: underline;

				content: 'Go to project website';
				font-size: small;
				transition-duration: 0.3s;
				opacity: 0.5;
			}
		}

		& .description {
			padding-top: 2rem;
			flex: 1;
			padding: 1rem;
		}
	}
	:global(.project-label) {
		margin-right: 0.1em;
		text-align: center;
		border-radius: 0.5em;
		padding: 0.2em;
		background-color: #ff3e00;
		color: #fff !important;
	}
	img,
	video {
		margin-top: 1rem;
		margin-right: 0.5em;
		max-height: 70%;
		max-width: 100%;
		/* border-right: 20px solid black; */
		align-self: center;
		border-radius: 10px;
	}
	iframe {
		min-width: 100%;
		min-height: 100%;
		zoom: 100%;

		position: absolute;
		top: 0;
		left: 0;
	}
	iframe::after .code {
		flex: 1;
	}
	.technologies {
		padding: 1.5em;
		// padding-right: 1em;
		transform: scale(0.85);
		border: 1px solid theme.$main;
		border-radius: 20px;
	}
</style>
