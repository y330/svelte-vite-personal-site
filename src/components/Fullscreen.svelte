<script>
	import { Button } from 'attractions'

	import { onMount } from 'svelte'
	import { Maximize2Icon, Minimize2Icon } from 'svelte-feather-icons'

	// define initial component state
	let isFull = false
	let fsContainer = null

	// boring plain js fullscreen support stuff below
	const noop = () => {}

	const fullscreenSupport = !!(
		document.fullscreenEnabled ||
		document.webkitFullscreenEnabled ||
		document.mozFullScreenEnabled ||
		document.msFullscreenEnabled ||
		false
	)

	const exitFullscreen = (
		document.exitFullscreen ||
		document.mozCancelFullScreen ||
		document.webkitExitFullscreen ||
		document.msExitFullscreen ||
		noop
	).bind(document)

	const requestFullscreen = () => {
		const requestFS = (
			fsContainer.requestFullscreen ||
			fsContainer.mozRequestFullScreen ||
			fsContainer.webkitRequestFullscreen ||
			fsContainer.msRequestFullscreen ||
			noop
		).bind(fsContainer)
		requestFS()
	}

	onMount(() => {
		// Add the icon stylesheet dynamically
		const link = document.createElement('link')
		link.rel = 'stylesheet'
		link.href = 'https://fonts.googleapis.com/icon?family=Material+Icons'
		document.head.appendChild(link)

		// remove the link when component is unmounted
		return () => {
			link.parentNode.removeChild(link)
		}
	})

	// handler for the fullscreen button
	const fsToggle = () => {
		if (!fullscreenSupport) return

		if (isFull) {
			exitFullscreen()
		} else {
			requestFullscreen(fsContainer)
		}
		isFull = !isFull
	}

	const iconStates = [
		{ component: Maximize2Icon, props: { size: '24' } },
		{ component: Minimize2Icon, props: { size: '24' } },
	]

	// the icon name is computed automagically based
	// on the state of the screen
	$: icon = isFull ? iconStates[1] : iconStates[0]
</script>

<div class="fs" class:isFull bind:this={fsContainer}>
	<slot {isFull} />
	{#if fullscreenSupport}
		<Button
			primary
			style="z-index: 2z; background-color: rgb(255, 209, 185) !important"
			on:click={fsToggle}
		>
			<svelte:component this={icon.component} {...icon.props} />
Preview demo fullscreen
		</Button>
	{/if}
</div>

<style>
	.isFull {
		width: 100vw;
		height: 100vh;
		display: flex;
		align-items: center;
		justify-content: center;
		background-color: #fff;
	}
</style>
