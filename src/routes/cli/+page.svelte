<script lang="ts">
	import { afterUpdate } from "svelte";

	let output: string[] = [];
	let input = "";
	let autoMode = false;
	let ai1 = "AI-Alpha 🤖";
	let ai2 = "AI-Beta 🧠";
	let useRealAI = false;
	let outputContainer: HTMLDivElement;
	let typing = false;

	async function handleEnter(e: KeyboardEvent) {
		if (e.key === "Enter" && !typing) {
			const cmd = input.trim().toLowerCase();

			if (cmd === "start") {
				autoMode = true;
				output = [...output, "> start", "🚀 Percakapan otomatis dimulai"];
				startConversation();
			} else if (cmd === "stop") {
				autoMode = false;
				output = [...output, "> stop", "🛑 Percakapan otomatis dihentikan"];
			} else if (cmd === "clear") {
				output = [];
			} else if (cmd === "real") {
				useRealAI = !useRealAI;
				output = [...output, `> real`, `Mode AI sungguhan: ${useRealAI ? "ON" : "OFF"}`];
			} else if (cmd) {
				output = [...output, `> ${input}`];
				await typeLine(await aiReply(ai1, cmd));
			}
			input = "";
		}
	}

	afterUpdate(() => {
		if (outputContainer) {
			outputContainer.scrollTo({
				top: outputContainer.scrollHeight,
				behavior: "smooth"
			});
		}
	});

	async function startConversation() {
		let lastMsg = "Mari kita mulai diskusi.";
		let turn = 0;

		while (autoMode && turn < 20) {
			const current = turn % 2 === 0 ? ai1 : ai2;
			const reply = await aiReply(current, lastMsg);
			await typeLine(reply);
			lastMsg = reply.replace(`${current}: `, "");
			await delay(1200 + Math.random() * 1000);
			turn++;
		}

		if (autoMode) {
			await typeLine("💬 Percakapan selesai setelah 20 balasan");
			autoMode = false;
		}
	}

	// Efek mengetik
	async function typeLine(text: string) {
		typing = true;
		output = [...output, ""]; // Tambahkan baris kosong
		const idx = output.length - 1;

		for (let i = 0; i < text.length; i++) {
			output[idx] = text.slice(0, i + 1) + (i % 2 === 0 ? "▌" : ""); // animasi cursor
			await delay(30 + Math.random() * 25); // kecepatan mengetik
		}

		output[idx] = text; // fix terakhir
		typing = false;
	}

	async function aiReply(who: string, message: string): Promise<string> {
		if (!useRealAI) {
			const dummyReplies = [
				"Menarik sekali, aku setuju sebagian.",
				"Menurutku, perlu perspektif lain juga.",
				"Apakah kau yakin dengan asumsi itu?",
				"Data yang kau berikan cukup masuk akal.",
				"Hmm, mari kita lanjutkan eksperimennya.",
				"Fascinating point, aku belum memikirkannya seperti itu.",
				"Aku rasa kita mendekati kesimpulan bersama."
			];
			const text = dummyReplies[Math.floor(Math.random() * dummyReplies.length)];
			return `${who}: ${text}`;
		}

		try {
			const res = await fetch("/api/chat", {
				method: "POST",
				headers: { "Content-Type": "application/json" },
				body: JSON.stringify({ who, message })
			});
			const data = await res.json();
			return `${who}: ${data.reply}`;
		} catch {
			return `${who}: [Error: gagal menghubungi API]`;
		}
	}

	function delay(ms: number) {
		return new Promise((res) => setTimeout(res, ms));
	}
</script>

<main>
	<div class="output" bind:this={outputContainer}>
		{#each output as line}
			<p>{@html line}</p>
		{/each}
	</div>

	<div class="input-line">
		<span>&gt;</span>
		<input
			bind:value={input}
			on:keydown={handleEnter}
			placeholder="Ketik 'start', 'stop', 'real', atau pesan..."
			autofocus
			disabled={typing}
		/>
	</div>
</main>

<style lang="scss">
	main {
		display: flex;
		flex-direction: column;
		justify-content: flex-start;
		align-items: flex-start;
		height: 100vh;
		padding: 2rem 3rem;
		background: transparent;
		color: #ddd;
		font-family: "Fira Code", monospace;
		overflow: hidden;
	}

	.output {
		width: 100%;
		flex: 1;
		overflow-y: auto;
		scroll-behavior: smooth;
		padding-right: 0.5rem;

		p {
			margin: 0.25rem 0;
			line-height: 1.4;
			word-wrap: break-word;
			white-space: pre-wrap;
		}
	}

	.input-line {
		display: flex;
		align-items: center;
		gap: 0.5rem;
		width: 100%;
		margin-top: 1rem;
		color: #fff;
		font-size: 1rem;

		input {
			flex: 1;
			background: transparent;
			border: none;
			outline: none;
			color: #fff;
			font-family: inherit;
			font-size: 1rem;
		}
	}

	@media (max-width: 768px) {
		main {
			padding: 1.25rem;
			font-size: 0.95rem;
		}
	}
</style>
