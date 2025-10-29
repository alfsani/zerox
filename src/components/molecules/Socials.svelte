<script>
	import Social from '../atoms/Social.svelte';
	import { TwitterIcon } from '@indaco/svelte-iconoir/twitter';
	import { TelegramIcon } from '@indaco/svelte-iconoir/telegram';
</script>

<div class="socials-container">
	<!-- Twitter -->
	<Social tip="Twitter" link="https://x.com/zeroxsociety">
		<TwitterIcon color="var(--accent)" size="22px" />
	</Social>

	<!-- Telegram -->
	<Social tip="Telegram" link="https://t.me/zeroxsociety">
		<TelegramIcon color="var(--accent)" size="22px" />
	</Social>

	<!-- DexScreener -->
	<Social tip="DexScreener" link="#">
		<img src="/dexscreener.svg" alt="DexScreener" class="icon" />
	</Social>

	<!-- Whitepaper (di samping kanan) -->
	<Social tip="Whitepaper" link="/whitepaper.pdf">
		<img src="/whitepaper.svg" alt="Whitepaper" class="icon" />
	</Social>
</div>

<style>
	.socials-container {
		display: flex;
		flex-direction: row; /* ikon sejajar ke samping */
		gap: 0.75rem;
		align-items: center;
	}

	.icon {
		width: 22px;
		height: 22px;
		object-fit: contain;
		vertical-align: middle;
		fill: var(--accent);
		opacity: 0.9;
		transition: transform 0.2s ease;
	}

	.icon:hover {
		transform: scale(1.05);
		opacity: 0.9;
	}
</style>
