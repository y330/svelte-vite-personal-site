<script>
	// Component
	import Icon from '@iconify/svelte'
	import { Card, Divider } from 'attractions'
	// Svelte
	import { fly } from 'svelte/transition'
	// Utils

	let projects = [
		{
			label: 'Essay Writer Bot',
			date: '2022-01-06',
			desc: "Artifical Intelligence essay writer that uses OpenAI’s GPT‑3 to write long-style essays whose prompts would normally excced the token limit for GPT-3. Github repo: <a href='https://github.com/y330/essaybot/' target='_blank'>Go to project</a>",
		},
		{
			label: 'FragmentQR',
			date: '2021-09-05',
			desc: "Browser extension that allows for the generation of QR codes linking to arbitrary text on a page.  <a style='color:lightgray' href='#'>Read more</a> <br><a href='https://bit.ly/FQRInstall'>Go to project.</a>",
		},
		{
			label: 'QuickSum',
			date: '2021-09-25',
			desc: "Quick text summarization tool, with a beautiful UI.  <a style='color:lightgray' href='https://github.com/y330/quicksum'>Read more</a> <br><a href='https://quicksum.vercel.app'>Go to project.</a>",
		},
		{
			label: 'Sveltekit + TailwindCSS Blog on Dystopian Literature',
			date: '2021-09-25',
			desc: "Blog on various dystopian texts, coded with SvelteKit, tailwind.css with Daisy UI components, and Graph CMS.  <a style='color:lightgray' href='#'>Read more</a><br> <a href='https://yonahs-fst.vercel.app'>Go to Project</a>",
		},
		{
			label: 'Q-Article Audio',
			date: '2021-08-01',
			desc: "Chrome extension to let you listen to an article as a podcast in the browser or optionally on your phone by scanning a QR code while in the middle of an article/webpage.  <a style='color:lightgray' href='#'>Read more<a> <br> <a href='https://y330.github.io/q-article-audio'>Go to Project</a>",
		},
	]
	let expanded = false

</script>

<section>
	<Divider text="Recent Projects" />
	<div class="recent-projects">
		{#each projects as proj}
			<div class="accordion-item" class:active={expanded === proj.label}>
				<button
					style="transition:all 300ms ease; padding: 1em;"
					class:active={expanded === proj.label}
					on:click={() => {
						expanded = proj.label
					}}
				>
					<div>
						<b>{proj.label}</b>
						<code>
							<Icon icon="tabler:clock" width="10" />
							{proj.date}}</code
						>
					</div>
					<div>
						{#if expanded === proj.label}
							<Icon
								icon="tabler:layout-navbar-expand-filled"
								width="25"
							/>
						{:else}
							<Icon
								icon="tabler:layout-navbar-collapse"
								width="25"
							/>
						{/if}
					</div>
				</button>

				{#if expanded === proj.label}
					<div
						class="info"
						in:fly={{ x: -200, duration: 1500 }}
						out:fly={{ x: 50, duration: 500 }}
					>
						<Card outline tight>
							<p>
								{@html proj.desc}
							</p></Card
						>
					</div>
				{/if}
			</div>
		{/each}
	</div>
</section>

<style lang="scss">
	@import 'theme.scss';
	.recent-projects {
		width: 90vw;
	}
	.accordion-item {
	}
	button {
		border-radius: 10px;
		text-align: left;
		background-color: rgba(0, 0, 0, 0.08);
		color: #656565;
		min-width: 100%;
		display: flex;
		margin-top: 1em;
		flex-direction: row;
		justify-content: space-between;
		border: none;

		code {
			// margin-left: 100%;
			color: #848484;
		}

		:hover {
			cursor: pointer;
		}
	}
	.active {
		& button {
			background-color: $main;
			color: #fff;
			transition: all 300ms ease;
			code {
				color: red;
			}
		}
	}
	.info {
		margin-bottom: 2rem;
		word-wrap: break-word;
		p {
			padding-inline: 10px;
			padding-bottom: 1em;
		}
	}
</style>
