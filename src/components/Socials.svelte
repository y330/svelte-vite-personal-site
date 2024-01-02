<script>
	// Components
	import Icon from '@iconify/svelte'
	import {
		Dialog,
		FormField,
		TextField,
		Button,
		Modal,
		Label,
	} from 'attractions'

	let contactForm = {
		show: false,
		sendEmails: true,
		subject: '',
		email: 'avivyonah@gmail.con',
		name: 'Yonah Aviv',
	}
</script>

<Button
	class="contact-btn"
	on:click={() => {
		contactForm.show = !contactForm.show
	}}><b>Contact me</b></Button
>

<div class="row">
	<Label>@</Label>

	<Button
		href="https://github.com/y330"
		title="Yonah Aviv on GitHub"
		neutral
		round
		class="github"
	>
		<Icon icon="tabler:brand-github" color="#ff3e00" width="22" />
	</Button>
	<Label>@</Label>

	<Button
		href="https://linkedin.com/in/yonahaviv"
		round
		class="linkedin"
		title="Yonah Aviv on Linkedin"
		neutral
	>
		<Icon icon="tabler:brand-linkedin" color="#ff3e00" width="22" />
	</Button>
</div>
{#if contactForm.show}
	<Modal bind:open={contactForm.show} let:closeCallback>
		<Dialog title="Contact me" {closeCallback}>
			<FormField name="Subject" help="i.e. Job Offer" required>
				<TextField bind:value={contactForm.subject} />
			</FormField>

			<Button
				on:click={() => (
					(contactForm.show = false),
					open(
						'mailto:email@example.com?subject={contactForm.subject}',
					)
				)}
				filled>Send me an email</Button
			>
		</Dialog>
	</Modal>
{/if}

<style lang="scss">
	@use 'theme.scss';

	// Social Media Buttons

	div {
		align-self: center;
		display: flex;
		flex-direction: row;
		padding-right: 0.5em;

		:global(.linkedin),
		:global(.github) {
			display: flex;
			justify-content: center;
			flex-direction: row;
			align-self: flex-end;
			flex-wrap: nowrap;
			transition: 300ms ease-out;
			height: 8vh;
			width: 5vw;

			border: 0.125em theme.$main solid;

			& :global(svg) {
				transition: all 300ms ease-in;
				fill: theme.$main;
				stroke: theme.$main;
				border-color: theme.$main;
			}

			&:hover {
				// width: 6vh;
				// float: right;
				// padding: 0.5em;

				& :global(svg) {
					color: white !important;
					stroke: white;
					fill: white;
				}
			}
			&:active {
				opacity: 0.7;
			}
			&:focus {
				opacity: 0.9;
			}
		}
		:global(.github) {
			margin-right: 0.25em;

			&:hover {
				border-color: black;
				background-color: black !important;
			}
		}
		:global(.linkedin) {
			&:hover {
				background-color: #0a66c2 !important;
				border-color: #0a66c2;
			}
		}
	}
	:global(.contact-btn) {
		font-size: medium !important;
		align-self: center;
		height: 10vh;
		padding-block: 0.75rem;
	}

	@media only screen and (max-width: 1025px) {
		.row {
			flex-direction: column;
			flex-wrap: wrap;
			:global(.btn) {
				margin-bottom: 10px;
				padding: 10%;
				margin: 0;
				width: 8vw;
			}
		}
		:global(.contact-btn) {
			height: 25%;
			width: 15vh;
			transform-origin: 50%;
			transform: rotate(90deg);
			font-size: 10px !important;
			align-self: center;
		}
	}
</style>
