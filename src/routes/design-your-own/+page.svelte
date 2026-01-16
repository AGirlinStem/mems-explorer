<script>
	let stiffness = 50;
	let gap = 30;
	let coupling = 70;

	// Reactive qualitative calculations
	$: systemGlow = (coupling / 100) * (stiffness / 50) * ( (100 - gap) / 100);
	$: waveSpeed = (110 - stiffness) / 20; 
</script>

<div class="page-container science-background" 
     style="--system-glow: {systemGlow}; --wave-speed: {waveSpeed}s;">
	
	<div class="content-wrapper">
		<header class="hero">
			<h1>Design Your Own MEMS UWB Power Sensor</h1>
			<div class="instruction-box panel">
				<p><strong>Goal:</strong> Adjust the design parameters below to find the perfect balance for your application. Watch the <strong>System Status</strong> to see how sensitivity and stability react.</p>
			</div>
		</header>

		<div class="main-layout">
			<div class="parameter-section">
				
				<section class="panel design-card">
					<div class="card-header">
						<span class="step-num">01</span>
						<h2>Diaphragm Stiffness</h2>
					</div>
					<div class="control-box">
						<input type="range" bind:value={stiffness} min="10" max="100" />
						<div class="range-labels">
							<span>Ultra-Thin (Sensitive)</span>
							<span>Thick (Robust)</span>
						</div>
					</div>
					<div class="description">
						<p>Controls the "flex" of the sensor. Thinner membranes detect smaller fields but are harder to stabilize.</p>
					</div>
				</section>

				<section class="panel design-card" class:warning={gap < 15}>
					<div class="card-header">
						<span class="step-num">02</span>
						<h2>Gap Distance</h2>
					</div>
					<div class="control-box">
						<input type="range" bind:value={gap} min="5" max="100" />
						<div class="range-labels">
							<span>Narrow (High Signal)</span>
							<span>Wide (Safe)</span>
						</div>
					</div>
					<div class="description">
						<p>The space between plates. Narrower gaps increase capacitance change but risk the plates sticking together (Pull-in).</p>
					</div>
				</section>

				<section class="panel design-card">
					<div class="card-header">
						<span class="step-num">03</span>
						<h2>Inductor Coupling</h2>
					</div>
					<div class="control-box">
						<input type="range" bind:value={coupling} min="0" max="100" />
						<div class="range-labels">
							<span>Low Intake</span>
							<span>High Intake</span>
						</div>
					</div>
					<div class="description">
						<p>Determines how much electromagnetic energy the sensor captures from the environment.</p>
					</div>
				</section>
			</div>

			<aside class="feedback-section">
				<div class="panel status-container">
					<h2>System Status</h2>
					
					<div class="visualizer-box">
						<div class="glow-orb"></div>
						<div class="wave-line"></div>
					</div>

					<div class="guide-box">
						<h3>Reading the Visuals:</h3>
						<ul>
							<li><strong>Glow Brightness:</strong> Represents signal sensitivity.</li>
							<li><strong>Wave Speed:</strong> Represents the mechanical response time.</li>
							<li><strong>Sensitivity Index:</strong> A qualitative score of your sensor's power.</li>
						</ul>
						<div class="score-display">
							Index: {(systemGlow * 10).toFixed(1)}
						</div>
					</div>
				</div>
			</aside>
		</div>
	</div>
</div>

<style>
	:global(body) {
		margin: 0;
		background-color: #02040a;
		color: #e0f7fa;
		font-family: 'Inter', sans-serif;
	}

	.science-background {
		background-color: #02040a;
		background-image: 
			repeating-linear-gradient(to right, rgba(94, 252, 244, calc(0.01 + (var(--system-glow) * 0.05))) 0px, transparent 1px, transparent 40px),
			repeating-linear-gradient(to bottom, rgba(94, 252, 244, calc(0.01 + (var(--system-glow) * 0.05))) 0px, transparent 1px, transparent 40px),
			radial-gradient(circle at center, rgba(94, 252, 244, calc(var(--system-glow) * 0.15)) 0%, transparent 70%),
			radial-gradient(ellipse at center, #051026 0%, #02040a 100%);
		min-height: 100vh;
	}

	.page-container { display: flex; flex-direction: column; align-items: center; padding: 40px 1.5rem; }
	.content-wrapper { width: 100%; max-width: 1100px; }

	.instruction-box { margin-top: 1rem; border-color: rgba(94, 252, 244, 0.4); text-align: center; }
	.instruction-box p { margin: 0; font-size: 0.95rem; opacity: 0.9; }

	.main-layout { display: grid; grid-template-columns: 1fr 380px; gap: 2rem; margin-top: 2rem; }

	.panel {
		background: rgba(12, 15, 35, 0.7);
		border: 1px solid rgba(94, 252, 244, 0.15);
		border-radius: 16px;
		backdrop-filter: blur(12px);
		padding: 1.5rem;
		margin-bottom: 1.2rem;
	}

	.range-labels { display: flex; justify-content: space-between; font-size: 0.7rem; opacity: 0.6; margin-top: 0.5rem; }
	.description p { font-size: 0.85rem; line-height: 1.4; opacity: 0.7; border-top: 1px solid rgba(255,255,255,0.1); padding-top: 0.8rem; margin-top: 1rem; }

	.visualizer-box { height: 180px; background: rgba(0,0,0,0.5); border-radius: 10px; position: relative; overflow: hidden; display: flex; align-items: center; justify-content: center; margin: 1rem 0; }
	.glow-orb { width: 80px; height: 80px; background: #5efcf4; filter: blur(40px); border-radius: 50%; opacity: calc(0.1 + var(--system-glow)); }
	.wave-line { position: absolute; width: 100%; height: 2px; background: linear-gradient(90deg, transparent, #5efcf4, transparent); animation: scan var(--wave-speed) linear infinite; }

	@keyframes scan { 0% { transform: translateY(-90px); opacity: 0; } 50% { opacity: 0.5; } 100% { transform: translateY(90px); opacity: 0; } }

	.guide-box h3 { font-size: 0.9rem; margin-bottom: 0.8rem; color: #5efcf4; }
	.guide-box ul { padding-left: 1.2rem; font-size: 0.8rem; opacity: 0.8; }
	.guide-box li { margin-bottom: 0.5rem; }

	.score-display { text-align: center; font-size: 1.5rem; font-weight: bold; color: #5efcf4; margin-top: 1.5rem; padding-top: 1rem; border-top: 1px solid rgba(94, 252, 244, 0.2); }

	.warning { border-color: #ff4444; box-shadow: 0 0 15px rgba(255, 68, 68, 0.1); }
	input[type="range"] { width: 100%; accent-color: #5efcf4; cursor: pointer; }
	h1 { text-align: center; color: #5efcf4; text-transform: uppercase; letter-spacing: 0.1rem; margin: 0; }

	@media (max-width: 900px) { .main-layout { grid-template-columns: 1fr; } }
</style>