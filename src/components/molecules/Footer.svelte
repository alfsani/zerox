<script>
	import Tooltip from '../atoms/Tooltip.svelte';
	import Socials from './Socials.svelte';
</script>

<hr />

<footer class="wrapper">
	<Socials />
	<h6>
		Made with pain. &#60;3
		<Tooltip tip="how to delete">
			<a href="" target="_blank" rel="noreferrer"></a>
		</Tooltip>
	</h6>
</footer>

<style lang="scss">
	hr {
		background-color: var(--elevation-one);
		height: 1px;
		border: 0;
		width: 100%;
		margin: 2rem 0;

		@media screen and (max-width: 768px) {
			margin: 1.5rem 0;
		}
	}

	footer.wrapper {
		display: flex;
		justify-content: space-between;
		align-items: center;
		padding: 1rem 0 2.5rem;
		color: var(--text-secondary);
		font-family: var(--font-two);
		font-size: 0.9rem;
		width: 100%;

		@media (max-width: 768px) {
			flex-direction: column;
			gap: 0.8rem;
			padding-bottom: 5rem; /* biar tidak nabrak navbar bawah */
			text-align: center;
		}
	}

	h6 {
		margin: 0;
		line-height: 1.8rem;
		color: var(--text-secondary);
		font-weight: 400;

		a {
			margin-left: 0.4rem;
			text-decoration: none;
			color: var(--accent);
			transition: color 0.3s ease;

			&:hover {
				color: var(--text-primary);
			}
		}
	}

	span {
		font-family: var(--font-two);
		background-color: var(--elevation-one);
		border-radius: 7px;
		padding: 0.15rem 0.5rem;
		margin-left: 1rem;
		margin-right: 0.4rem;
	}

	/* biar icon sosmed tidak terlalu besar di mobile */
	:global(.socials-container) {
		display: flex;
		gap: 1rem;

		@media (max-width: 768px) {
			gap: 0.75rem;

			svg {
				width: 20px;
				height: 20px;
			}
		}
	}
</style>
