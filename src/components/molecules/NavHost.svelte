<script lang="ts">
	import Nav from '../atoms/Nav.svelte';
	import { page } from '$app/stores';

	let y: number;
	$: currentPath = $page.url.pathname;
</script>

<nav>
	<div class:scrolled={y > 20}>
		<ul>
			<!-- 🏠 Home -->
			<Nav href="#home" section="/" isSelected={currentPath === '/' && y < 350}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="var(--accent)" viewBox="0 0 24 24">
					<path fill="none" d="M0 0h24v24H0z" />
					<path d="M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z" />
				</svg>
			</Nav>

			<!-- ℹ️ About -->
			<Nav href="#about" section="about" isSelected={currentPath === '/' && y > 350 && y < 675}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="var(--accent)" viewBox="0 0 24 24">
					<path fill="none" d="M0 0h24v24H0z" />
					<path d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10
						10-4.48 10-10S17.52 2 12 2zm1 15h-2v-6h2v6zm0-8h-2V7h2v2z"/>
				</svg>
			</Nav>

			<!-- 🖼️ Collections -->
			<Nav href="#aw" section="collections" isSelected={currentPath === '/' && y > 675 && y < 1000}>
				<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="var(--accent)" viewBox="0 0 24 24">
					<path fill="none" d="M0 0h24v24H0z" />
					<path d="M20 6h-4V4c0-1.11-.89-2-2-2h-4c-1.11 0-2
						.89-2 2v2H4c-1.11 0-1.99.89-1.99 2L2
						19c0 1.11.89 2 2 2h16c1.11 0 2-.89
						2-2V8c0-1.11-.89-2-2-2zm-6 0h-4V4h4v2z"/>
				</svg>
			</Nav>

			<!-- 🧠 CLI -->
		<!-- 🧠 Backroms -->
<Nav href="/backrooms" section="backrooms" isSelected={currentPath === '/backrooms'}>
	<svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="var(--accent)" viewBox="0 0 24 24">
		<path fill="none" d="M0 0h24v24H0z" />
		<path d="M4 4h16a2 2 0 012 2v12a2 2 0 01-2
			2H4a2 2 0 01-2-2V6a2 2 0 012-2zm4
			3h8v2H8V7zm0 4h8v2H8v-2zm0 4h5v2H8v-2z"/>
	</svg>
</Nav>

		</ul>
	</div>
</nav>

<svelte:window bind:scrollY={y} />

<style lang="scss">
	nav {
		display: flex;
		align-items: center;
		justify-content: center;
	}

	div {
		width: 100%;
		position: fixed;
		top: 0;
		left: 0;
		z-index: 15;
		padding: 1rem 0;
		background-color: var(--bg-color);
		backdrop-filter: blur(15px);
		-webkit-backdrop-filter: blur(15px);
		background-blend-mode: overlay;
		transition: all 0.5s ease;

		ul {
			display: flex;
			justify-content: space-evenly;
			align-items: center;
			gap: 1.5rem;
			margin: 0 auto;
			padding: 0;
			width: 100%;
			max-width: 600px;
		}
	}

	/* === SCROLLED === */
	.scrolled {
		background-color: var(--elevation-five);
		box-shadow: 0px 8px 20px rgba(0, 0, 0, 0.3);
		padding: 0.6rem 0;
		transition: all 0.3s ease;
	}

	/* === DESKTOP === */
	@media (min-width: 868px) {
		div {
			width: auto;
			border-radius: 12px;
			top: 1rem;
			padding: 0.75rem 1.25rem;
		}

		ul {
			gap: 2rem;
			max-width: 500px;
		}

		.scrolled {
			border: 1.5px solid var(--accent-opacity);
			box-shadow: 0px 15px 8px -10px rgba(0, 0, 0, 0.4);
			background-color: var(--elevation-five);
		}
	}

	/* === MOBILE === */
	@media (max-width: 868px) {
		div {
			top: auto;
			bottom: 0;
			padding: 0.3rem 0;
			background-color: var(--elevation-one);
			border-top: 1px solid var(--accent-opacity);
		}

		ul {
			gap: 0.5rem;
			padding: 0.25rem 0.5rem;
			width: 100%;
			justify-content: space-around;
		}
	}
</style>
