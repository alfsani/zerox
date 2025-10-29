<script lang="ts">
	import { goto } from '$app/navigation';
	import { page } from '$app/stores';

	export let href = '#';
	export let section = 'home';
	export let isSelected: boolean;

	$: currentPage = $page.url.pathname;

	async function handleClick() {
		if (href.startsWith('/')) {
			await goto(href);
			return;
		}

		if (currentPage === '/') {
			const el = document.querySelector(href);
			if (el) el.scrollIntoView({ behavior: 'smooth' });
		} else {
			window.location.href = `/${href}`;
		}
	}
</script>

<li class:selected={isSelected}>
	<button on:click={handleClick}>
		<div class="icon-container">
			<slot />
		</div>
		<h5>{section}</h5>
	</button>
</li>

<style lang="scss">
	li {
		list-style: none;
	}

	button {
		background-color: transparent;
		border: none;
		color: var(--text-secondary);
		font-size: 1rem;
		user-select: none;
		display: flex;
		align-items: center;
		gap: 0.6rem;
		padding: 10px 18px;
		border-radius: 50px;
		cursor: pointer;
		transition:
			background-color 0.3s var(--bezier-one),
			transform 0.3s var(--bezier-one);

		&:hover {
			background-color: var(--elevation-three);
			color: var(--accent);
		}
	}

	h5 {
		transition: color 0.3s ease, opacity 0.3s ease;
		opacity: 0.85;
		font-weight: 400;
	}

	.icon-container {
		display: none;
	}

	.selected h5 {
		color: var(--accent);
		opacity: 1;
		font-weight: 500;
	}

	/* === DESKTOP === */
	@media (min-width: 869px) {
		button {
			font-size: 1rem;
			padding: 10px 22px;
		}
	}

	/* === MOBILE === */
	@media (max-width: 868px) {
		button {
			flex-direction: column;
			align-items: center;
			justify-content: center;
			gap: 0.3rem;
			padding: 8px 12px;
			font-size: 0.8rem;
		}

		h5 {
			margin: 0;
			font-size: 0.75rem;
		}

		.icon-container {
			display: block;
			padding: 6px 14px;
			border-radius: 50%;
			background-color: transparent;
			transition: background-color 0.4s var(--bezier-one);
		}

		button:hover .icon-container,
		.selected .icon-container {
			background-color: var(--accent-opacity);
		}
	}
</style>
