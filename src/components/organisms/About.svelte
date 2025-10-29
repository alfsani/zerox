<script lang="ts">
	import { onMount } from 'svelte';
	import RichPresence from '../molecules/RichPresence.svelte';
	import Tooltip from '../atoms/Tooltip.svelte';

	// ===== Efek mengetik otomatis =====
	let fullText = `Zerox is a basic implementation of AGI technology. It is not designed to perform specific tasks, but instead acts and behaves based on its own desires. This web interface was built to allow users to interact with the AGI and observe how it forms its own body.
`;

	let displayedText = '';
	let index = 0;
	let typingSpeed = 25; // kecepatan mengetik (ms per huruf)

	function typeWriter() {
		if (index < fullText.length) {
			displayedText += fullText.charAt(index);
			index++;
			setTimeout(typeWriter, typingSpeed);
		}
	}

	onMount(() => {
		typeWriter();
	});

	// ===== Hitung umur dinamis =====
	let getAge = () => {
		let birthDate = new Date('2007/03/24');
		const ageMs = Date.now() - birthDate.getTime();
		const preciseAge = (ageMs / 31536000000).toFixed(10);
		return preciseAge;
	};

	let age = getAge();
	setInterval(() => {
		age = getAge();
	}, 1000);
</script>

<section id="about" class="wrapper">
	<div>
		<RichPresence />
	</div>

	<div class="text">
		<h2>what is more secret than zerox?</h2>

		<!-- efek mengetik otomatis -->
		<p class="typing">
			{displayedText}
		</p>

		<!-- contoh tambahan: umur real-time -->
		
	</div>
</section>

<style lang="scss">
	@import '../../styles/mixins.scss';

	section {
		margin-bottom: 6rem;
		display: grid;
		gap: 4.5rem;
		grid-template-columns: 1fr 1fr;
		align-items: center;
	}

	.text {
		position: relative;
		line-height: 1.75rem;
	}

	.typing {
		font-family: var(--font-two);
		white-space: pre-line; /* biar tetap ada baris baru */
		border-right: 2px solid var(--accent);
		animation: blink 0.75s step-end infinite;
		font-size: 0.95rem;
	}

	.age {
		margin-top: 1rem;
		color: var(--text-secondary);
	}

	@keyframes blink {
		from, to {
			border-color: transparent;
		}
		50% {
			border-color: var(--accent);
		}
	}

	.text::before {
		@include outlineText(
			$content: 'xxx',
			$translateX: 97%,
			$translateY: -5%,
			$fontSize: 300px,
			$opacity: 0.22
		);
	}

	h2 {
		display: none;
		margin-top: 1rem;
	}

	@media (max-width: 868px) {
		section {
			display: flex;
			flex-direction: column;
			align-items: normal;
		}

		h2 {
			display: block;
			margin-bottom: 1rem;
		}
	}
</style>
