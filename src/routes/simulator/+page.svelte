<script>
	/* =========================
	   TRANSITION (SAME AS HERO)
	   ========================= */

	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';

	let mounted = false;

	onMount(() => {
		mounted = true;
	});

	/* =========================
	   SIMULATOR LOGIC
	   ========================= */

	let field = 0.8;
	const sensitivity = 4.5 / 0.8;
	$: deltaC = field * sensitivity;
	$: deflection = field * 10;
</script>

<div class="simulator-page">
	{#if mounted}
		<div
			class="content-wrapper"
			in:fly={{ y: 50, duration: 1000 }}
		>
			<section class="simulator-ui">
				<h2>MEMS Sensor Simulator</h2>

				<div class="panel">
					<label>
						Incident field (µA/m): {field.toFixed(2)}
						<input
							type="range"
							min="0"
							max="5"
							step="0.1"
							bind:value={field}
						/>
					</label>

					<p>
						Capacitance Change:
						<strong>{deltaC.toFixed(2)} aF</strong><br />
						Diaphragm Deflection:
						<strong>{deflection.toFixed(2)} pm</strong>
					</p>

					<svg width="220" height="120" viewBox="0 0 220 120">
						<rect
							x="20"
							y="20"
							width="180"
							height="80"
							fill="none"
							stroke="var(--accent)"
							stroke-width="2"
						/>
						<rect
							x="20"
							y={20 + deflection / 5}
							width="180"
							height="80"
							fill="rgba(94,252,244,0.2)"
							stroke="rgba(94,252,244,0.8)"
							stroke-width="1"
						/>
					</svg>

					<p class="hint">
						Move the slider to simulate stronger EM fields bending the membrane.
					</p>
				</div>
			</section>

			<section class="panel idea-card">
				<h1>Idea</h1>
				<p>
					This tool models how an incoming EM field interacts with a MEMS diaphragm.
					As the field strength increases, the membrane deflects slightly, changing
					the distance between capacitor plates and shifting the capacitance.
				</p>
			</section>
		</div>
	{/if}
</div>

<style>
	/* --- PREVENT WHITE FLASH --- */
	:global(body) {
		background-color: #050716 !important;
		margin: 0;
		padding: 0;
	}

	.simulator-page {
		background: radial-gradient(circle at center, #0a133a 0%, #050716 100%);
		min-height: 100vh;
		width: 100%;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 120px 1rem 5rem 1rem;
		color: white;
	}

	.content-wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
		gap: 3rem;
		width: 100%;
		will-change: transform;
	}

	.simulator-ui {
		width: 100%;
		max-width: 600px;
		text-align: center;
	}

	.idea-card {
		max-width: 800px;
	}

	input[type='range'] {
		display: block;
		width: 100%;
		margin: 1rem 0;
		accent-color: var(--accent);
		cursor: pointer;
	}

	.hint {
		font-size: 0.9rem;
		opacity: 0.7;
		margin-top: 1rem;
	}

	h2 {
		letter-spacing: 0.2rem;
		text-transform: uppercase;
		margin-bottom: 1.5rem;
		text-shadow: var(--accent-glow);
	}

	.panel {
		background: rgba(12, 15, 35, 0.9);
		border: 1px solid var(--panel-border);
		padding: 2rem;
		border-radius: 12px;
	}
</style>
