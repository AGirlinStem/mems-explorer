<div class="page-container science-background">
	<div class="content-wrapper">
		
		<header class="hero">
			<h1>About the MEMS Sensor Simulator</h1>
			<div class="intro-panel panel">
				<p>This project is an interactive visualization of a microelectromechanical systems (MEMS) ultra-wideband (UWB) power sensor that converts invisible electromagnetic energy into measurable electrical signals through controlled mechanical motion.</p>
				<p class="disclaimer">The simulator is designed as a conceptual and educational tool to illustrate operating principles rather than to function as a fabrication-level or numerical simulation.</p>
			</div>
		</header>

		<div class="about-grid">
			
			<section class="panel info-card">
				<div class="card-icon"></div>
				<h2>Research Inspiration</h2>
				<p>The simulator is inspired by published academic research on MEMS ultra-wideband power sensors that integrate a <strong>planar loop inductor</strong> with a <strong>vibrating diaphragm variable capacitor</strong>.</p>
				<p>In this architecture, incoming UWB fields induce a voltage in the planar inductor, which acts as an integrated loop antenna. This generates an electrostatic force, causing a thin diaphragm to deflect by picometers: one trillionth of a meter.</p>
			</section>

			<section class="panel info-card">
				<div class="card-icon"></div>
				<h2>Why Mechanical Sensing?</h2>
				<p>Unlike conventional solid-state RF detectors, this sensor relies on <strong>mechanical inertia</strong> to achieve a frequency-independent RMS response.</p>
				<p>Because the electromagnetic frequencies are significantly higher than the diaphragm’s mechanical resonant frequency, the membrane responds only to the average (RMS) power of the incident field rather than following the instantaneous waveform.</p>
			</section>

			<section class="panel info-card full-width">
				<div class="card-icon"></div>
				<h2>Why a Simulator?</h2>
				<p>At the physical scale, diaphragm deflections occur at picometer levels and capacitance changes are measured in <strong>attifarads</strong>. These effects are impossible to observe directly.</p>
				<p>This simulator magnifies and visualizes those interactions to make the underlying physics intuitive and accessible, bridging the gap between electromagnetic theory and MEMS mechanics.</p>
			</section>
		</div>

		<section class="panel reference-panel">
			<h2>References and Attribution</h2>
			<div class="citation">
				<p class="author">S. Vejella and S. Chowdhury</p>
				<p class="title">“A MEMS Ultra-Wideband (UWB) Power Sensor with a Fe-Co-B Core Planar Inductor and a Vibrating Diaphragm Capacitor”</p>
				<p class="journal">Sensors, 2021</p>
			</div>
			<p class="univ-credit">The original device concept and theoretical framework were developed within the <strong>Electrical and Computer Engineering Department, University of Windsor</strong>.</p>
		</section>

		<footer class="project-credit">
			<p>Project Visualization, Interface Design, and Conceptual Modeling</p>
			<h3>Naimah Ishaque</h3>
		</footer>

	</div>
</div>

<style>
	:global(body) {
		margin: 0;
		background-color: #02040a;
		color: #e0f7fa;
		font-family: 'Inter', sans-serif;
	}

	/* SCIENTIFIC THEMED BACKGROUND */
	.science-background {
		background-color: #02040a;
		background-image: 
			repeating-linear-gradient(to right, rgba(94, 252, 244, 0.03) 0px, transparent 1px, transparent 40px),
			repeating-linear-gradient(to bottom, rgba(94, 252, 244, 0.03) 0px, transparent 1px, transparent 40px),
			radial-gradient(circle at 50% 30%, rgba(94, 252, 244, 0.07) 0%, transparent 60%),
			radial-gradient(ellipse at center, #051026 0%, #02040a 100%);
		background-attachment: fixed;
		min-height: 100vh;
	}

	.page-container {
		display: flex;
		flex-direction: column;
		align-items: center;
		padding: 80px 1.5rem;
	}

	.content-wrapper { width: 100%; max-width: 900px; }

	/* PANEL STYLING */
	.panel {
		background: rgba(12, 15, 35, 0.7);
		border: 1px solid rgba(94, 252, 244, 0.15);
		border-radius: 20px;
		backdrop-filter: blur(12px);
		padding: 2rem;
		margin-bottom: 2rem;
	}

	.hero { text-align: center; margin-bottom: 4rem; }
	h1 { font-size: 2.5rem; color: #5efcf4; text-transform: uppercase; letter-spacing: 0.15rem; margin-bottom: 1.5rem; }
	
	.intro-panel p { font-size: 1.1rem; line-height: 1.6; opacity: 0.9; }
	.disclaimer { font-size: 0.85rem; color: #5efcf4; margin-top: 1rem; opacity: 0.7; }

	.about-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 1.5rem; }
	.full-width { grid-column: span 2; }

	h2 { font-size: 1.4rem; color: #5efcf4; margin-bottom: 1rem; letter-spacing: 0.05rem; }
	p { line-height: 1.6; opacity: 0.8; margin-bottom: 1rem; }
	.card-icon { font-size: 2rem; margin-bottom: 1rem; }

	/* CITATION STYLING */
	.reference-panel { text-align: center; }
	.citation { border-left: 3px solid #5efcf4; padding-left: 1.5rem; margin: 2rem 0; text-align: left; }
	.author { font-weight: bold; color: white; margin: 0; }
	.title { font-style: italic; color: #5efcf4; margin: 0.5rem 0; }
	.journal { font-size: 0.9rem; opacity: 0.6; }
	.univ-credit { font-size: 0.85rem; border-top: 1px solid rgba(255,255,255,0.1); padding-top: 1.5rem; }

	/* FOOTER */
	.project-credit { text-align: center; margin-top: 4rem; padding-bottom: 2rem; }
	.project-credit p { font-size: 0.8rem; text-transform: uppercase; letter-spacing: 0.2rem; margin-bottom: 0.5rem; }
	.project-credit h3 { font-size: 1.8rem; color: white; margin: 0 0 2rem 0; letter-spacing: 0.1rem; }
	.back-link { color: #5efcf4; text-decoration: none; font-weight: bold; transition: opacity 0.3s; }
	.back-link:hover { opacity: 0.7; }

	@media (max-width: 768px) {
		.about-grid { grid-template-columns: 1fr; }
		.full-width { grid-column: span 1; }
	}
</style>