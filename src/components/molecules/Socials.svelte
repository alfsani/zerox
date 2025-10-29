<script>
	import Social from '../atoms/Social.svelte';

	// import dua ikon dari iconoir
	import { TwitterIcon } from '@indaco/svelte-iconoir/twitter';
	import { TelegramIcon } from '@indaco/svelte-iconoir/telegram';
</script>

<div class="socials-container">
	<!-- Twitter -->
	<Social tip="Twitter" link="https://twitter.com/username_kamu">
		<TwitterIcon color="var(--accent)" size="22px" />
	</Social>

	<!-- Telegram -->
	<Social tip="Telegram" link="https://t.me/username_kamu">
		<TelegramIcon color="var(--accent)" size="22px" />
	</Social>

	<!-- DexScreener -->
	<Social tip="DexScreener" link="https://dexscreener.com/yourtokenlink">
		<img src="/dexscreener.svg" alt="DexScreener" class="icon" />
	</Social>
</div>

<style>
	.socials-container {
		display: flex;
		gap: 0.75rem;
		align-items: center;
	}

	/* Style untuk ikon DexScreener */
.icon {
	width: 22px;
	height: 22px;
	object-fit: contain;
	vertical-align: middle;
	fill: var(--accent); /* 💥 ini yang penting: ubah warna jadi sama seperti ikon lain */
	opacity: 0.9; /* sedikit transparan saja biar lembut */
	transition: transform 0.2s ease;
}

.icon:hover {
	transform: scale(1.05);
	opacity: 0.9; /* tetap */
}




</style>
