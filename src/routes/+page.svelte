<script>
	import WaveBackground from '$lib/WaveBackground.svelte';
	import { fly } from 'svelte/transition';
	import { onMount } from 'svelte';

	let mounted = false;

	onMount(() => {
		mounted = true;
	});
</script>

<WaveBackground />

<div class="page-container">
	{#if mounted}
		<div class="content-wrapper" in:fly={{ y: 50, duration: 1000 }}>
			<section class="hero">
				<h1>See Invisible Waves Move Matter</h1>
				<p>Explore how electromagnetic fields bend microscopic membranes and produce measurable electrical signals</p>
			</section>

			<section class="panel idea-card">
				<p>Click on the simulator tab below to get a head start! ✨</p>
				<p>
					<a href="/simulator" class="btn-primary">
						▶ Try the Simulator
					</a>
				</p>
			</section>
		</div>
	{/if}
</div>

<style>
	.page-container {
		position: relative;
		z-index: 10;
		color: white;
		padding-top: 80px;
		display: flex;
		flex-direction: column;
		align-items: center;
		min-height: 100vh;
	}

	.content-wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
	}

	.hero {
		height: 40vh;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		text-align: center;
		padding: 0 1rem;
	}

	/* FIXED: Narrower border as requested */
	.idea-card {
		max-width: 500px; 
		margin: 2rem;
		text-align: center;
	}

	.btn-primary {
		display: inline-block;
		margin-top: 1rem;
		padding: 0.8rem 2rem;
		background: rgba(94, 252, 244, 0.1);
		border: 1px solid var(--accent);
		color: var(--accent);
		border-radius: 4px;
		text-decoration: none;
		font-weight: bold;
		text-transform: uppercase;
		letter-spacing: 0.1rem;
		transition: all 0.3s ease;
		text-shadow: var(--accent-glow);
	}

	.btn-primary:hover {
		background: var(--accent);
		color: #050716;
		box-shadow: var(--accent-glow);
		transform: translateY(-3px);
	}

	.panel {
		background: rgba(12, 15, 35, 0.85);
		border: 1px solid var(--panel-border);
		padding: 1.5rem 2rem;
		border-radius: 12px;
		box-shadow: var(--accent-glow);
		backdrop-filter: blur(10px);
	}
</style>