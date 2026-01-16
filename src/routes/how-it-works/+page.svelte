<script>
	import { onMount } from 'svelte';

	let loaded = false;
	onMount(() => {
		// Small timeout ensures the browser is ready to animate
		setTimeout(() => { loaded = true; }, 50);
	});
</script>

<div class="page-container">
	<div class="content-wrapper">
		
		<header class="hero">
			<p>Scroll below ↓</p>
		</header>

		<div class="explainer-container" class:loaded>
			
			<svg class="connection-lines" viewBox="0 0 100 100" preserveAspectRatio="none">
				<path 
					d="M 20,20 L 80,20 L 80,80 L 20,80 Z" 
					fill="none" 
					stroke="var(--accent)" 
					stroke-width="0.3" 
					stroke-dasharray="2,2"
				/>
			</svg>

			<div class="how-it-works-grid">
				<div class="step-card panel s1">
					<div class="step-icon">📡</div>
					<h3>Step 1: The Electromagnetic Field Arrives</h3>
					<p>An incoming radio or ultra wideband field travels through space carrying energy.
					When it reaches the MEMS device, part of that energy interacts with the thin diaphragm on the sensor.
					Even though we cannot see the field, it applies a very small force to the membrane.</p>
				</div>

				<div class="step-card panel s2">
					<div class="step-icon">⚡</div>
					<h3>Step 2: The Diaphragm Flexes</h3>
					<p>The diaphragm in the MEMS device behaves like a tiny flexible drumhead.
					When the field energy is absorbed, the membrane bends by a distance measured in picometers.
					A picometer is one trillionth of a meter.
					The motion is very small, but it is enough to change electrical properties.</p>
				</div>

				<div class="vision-card panel">
					<div class="vision-icon"></div>
					<h2>Vision</h2>
					<p>We aim to make the invisible world of wireless energy visible, measurable, and interactive.
					This project presents MEMS-based electromagnetic interactions through a clear and accessible simulation.</p>
				</div>

				<div class="step-card panel s3">
					<div class="step-icon">🌊</div>
					<h3>Step 3: Capacitance Changes</h3>
					<p>The diaphragm forms one plate of a capacitor.
					A capacitor stores electrical charge, and its value depends on the spacing between its plates.
					As the diaphragm moves closer or farther away, the capacitance changes.</p>
					<p>The basic relationship is: <i>C = (&epsilon; &times; A) / d</i></p>
					<p>If the distance decreases, capacitance increases. That change is what the simulator displays.</p>
				</div>

				<div class="step-card panel s4">
					<div class="step-icon">📊</div>
					<h3>Step 4: Turning Motion Into Signal</h3>
					<p>Electronics connected to the capacitor detect the tiny change in capacitance.
					Circuits can amplify, digitize, and process this variation.
					This allows a physical event, such as bending caused by a field, to be converted into information a computer can use.</p>
				</div>
			</div>
		</div>

		<section class="applications-section panel">
			<h2>Applications</h2>
			<ul class="app-list">
				<li>🔹 Wireless sensing</li>
				<li>🔹 Indoor positioning</li>
				<li>🔹 Wearable health devices</li>
				<li>🔹 IoT and smart homes</li>
				<li>🔹 Structural and environmental monitor</li>
				<li>🔹 Micro-robotics</li>
			</ul>
		</section>
	</div>
</div>

<style>
	:global(body) {
		background-color: #050716 !important;
		margin: 0;
		overflow-x: hidden;
	}

	.page-container {
		/* Points to your IMAGES folder inside static */
		background: 
			linear-gradient(rgba(5, 7, 22, 0.8), rgba(5, 7, 22, 0.8)), 
			url('/IMAGES/glowing-sphere.jpg'); 
		background-size: cover;
		background-position: center;
		background-attachment: fixed;
		
		min-height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 80px 1rem 5rem 1rem;
		color: white;
	}

	.content-wrapper {
		display: flex;
		flex-direction: column;
		align-items: center;
		width: 100%;
		max-width: 1100px;
		gap: 4rem;
	}

	.explainer-container {
		position: relative;
		width: 100%;
		padding: 2rem;
	}

	.how-it-works-grid {
		display: grid;
		grid-template-columns: 1fr 1fr 1fr;
		grid-template-rows: 1fr 1fr 1fr;
		gap: 2rem;
		align-items: center;
		justify-items: center;
	}

	.s1 { grid-area: 1 / 1 / 2 / 2; }
	.s2 { grid-area: 1 / 3 / 2 / 4; }
	.vision-card { grid-area: 2 / 2 / 3 / 3; z-index: 10; }
	.s3 { grid-area: 3 / 3 / 4 / 4; }
	.s4 { grid-area: 3 / 1 / 4 / 2; }

	.step-card {
		opacity: 0;
		transition: transform 0.8s cubic-bezier(0.34, 1.56, 0.64, 1), opacity 0.6s ease-out;
		pointer-events: none;
	}

	.s1 { transform: translate(110%, 110%) scale(0.8); }
	.s2 { transform: translate(-110%, 110%) scale(0.8); }
	.s3 { transform: translate(-110%, -110%) scale(0.8); }
	.s4 { transform: translate(110%, -110%) scale(0.8); }

	.loaded .step-card {
		opacity: 1;
		transform: translate(0, 0) scale(1);
		pointer-events: auto;
	}

	.loaded .s1 { transition-delay: 100ms; }
	.loaded .s2 { transition-delay: 300ms; }
	.loaded .s3 { transition-delay: 500ms; }
	.loaded .s4 { transition-delay: 700ms; }

	.panel {
		background: rgba(12, 15, 35, 0.9);
		border: 1px solid rgba(94, 252, 244, 0.3);
		border-radius: 20px;
		backdrop-filter: blur(10px);
	}

	.step-card {
		padding: 1.5rem;
		width: 100%;
		max-width: 250px;
		text-align: center;
	}

	.step-card:hover {
		transform: translateY(-8px) scale(1.03) !important;
		box-shadow: 0 0 25px rgba(94, 252, 244, 0.4);
		border-color: #5efcf4;
	}

	.vision-card {
		padding: 2rem;
		width: 100%;
		max-width: 350px;
		text-align: center;
		border-color: #5efcf4;
	}

	.connection-lines {
		position: absolute;
		top: 0; left: 0; width: 100%; height: 100%;
		z-index: 0;
		opacity: 0;
		transition: opacity 1s ease 1.2s;
	}

	.loaded .connection-lines { opacity: 0.3; }

	.step-icon, .vision-icon { font-size: 2rem; margin-bottom: 0.5rem; }
	h2 { color: #5efcf4; text-transform: uppercase; letter-spacing: 0.1rem; margin: 0; }
	h3 { font-size: 1rem; margin-bottom: 0.5rem; color: white; }
	p { font-size: 0.85rem; opacity: 0.8; line-height: 1.4; margin: 0.5rem 0; }

	.app-list {
		display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
		gap: 1rem; list-style: none; padding: 0; margin-top: 1.5rem; text-align: left;
	}

	@media (max-width: 900px) {
		.how-it-works-grid { display: flex; flex-direction: column; gap: 2rem; }
		.step-card { transform: translateY(20px) scale(0.9) !important; }
		.loaded .step-card { transform: translateY(0) scale(1) !important; }
		.connection-lines { display: none; }
	}
</style>