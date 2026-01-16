<script>
	import { onMount } from 'svelte';
	import * as THREE from 'three';
	import { EffectComposer } from 'three/examples/jsm/postprocessing/EffectComposer.js';
	import { RenderPass } from 'three/examples/jsm/postprocessing/RenderPass.js';
	import { UnrealBloomPass } from 'three/examples/jsm/postprocessing/UnrealBloomPass.js';

	let container;

	onMount(() => {
		const scene = new THREE.Scene();
		// Match the background color from your app.css precisely
		scene.fog = new THREE.FogExp2(0x050716, 0.02);

		const camera = new THREE.PerspectiveCamera(40, window.innerWidth / window.innerHeight, 0.1, 1000);
		camera.position.set(-15, 25, 50);
		camera.lookAt(15, 0, 0);

		// alpha: true is required so the CSS background doesn't hide the canvas
		const renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
		renderer.setClearColor(0x000000, 0); 
		renderer.setSize(window.innerWidth, window.innerHeight);
		renderer.setPixelRatio(window.devicePixelRatio);
		container.appendChild(renderer.domElement);

		const composer = new EffectComposer(renderer);
		composer.addPass(new RenderPass(scene, camera));
		const bloom = new UnrealBloomPass(new THREE.Vector2(window.innerWidth, window.innerHeight), 1.5, 0.4, 0.85);
		bloom.threshold = 0.1;
		bloom.strength = 1.8; 
		composer.addPass(bloom);

		// 1. The Traveling Wave Mesh (matches reference image)
		const geometry = new THREE.PlaneGeometry(120, 80, 85, 55);
		geometry.rotateX(-Math.PI / 2);
		
		const waveMaterial = new THREE.ShaderMaterial({
			uniforms: { uTime: { value: 0 }, uColor: { value: new THREE.Color(0x0066ff) } },
			vertexShader: `
				uniform float uTime;
				varying float vHeight;
				void main() {
					vec3 pos = position;
					float mask = smoothstep(35.0, -10.0, pos.x); 
					// Traveling waves math
					float wave = sin(pos.x * 0.18 - uTime * 2.2) * cos(pos.z * 0.12 + uTime) * 6.5;
					pos.y += wave * mask;
					vHeight = pos.y;
					gl_Position = projectionMatrix * modelViewMatrix * vec4(pos, 1.0);
				}
			`,
			fragmentShader: `
				uniform vec3 uColor;
				varying float vHeight;
				void main() {
					float brightness = smoothstep(-2.0, 5.0, vHeight) * 0.6 + 0.4;
					gl_FragColor = vec4(uColor * brightness, 0.45);
				}
			`,
			transparent: true,
			wireframe: true
		});
		const mesh = new THREE.Mesh(geometry, waveMaterial);
		scene.add(mesh);

		// 2. Data Squares
		const squareGeom = new THREE.PlaneGeometry(0.4, 0.4);
		const squareMat = new THREE.MeshBasicMaterial({ color: 0x5efcf4, side: THREE.DoubleSide, transparent: true, opacity: 0.8 });
		const instances = 1300;
		const instancedMesh = new THREE.InstancedMesh(squareGeom, squareMat, instances);
		scene.add(instancedMesh);

		const dummy = new THREE.Object3D();
		const animate = () => {
			const t = performance.now() * 0.001;
			waveMaterial.uniforms.uTime.value = t;

			for (let i = 0; i < instances; i++) {
				let x = (i % 45 - 22) * 2.6;
				let z = (Math.floor(i / 45) - 15) * 2.6;
				let mask = Math.max(0, Math.min(1, (x - 35.0) / (-10.0 - 35.0)));
				mask = mask * mask * (3 - 2 * mask);
				let y = (Math.sin(x * 0.18 - t * 2.2) * Math.cos(z * 0.12 + t) * 6.5 * mask) + 0.2;
				
				dummy.position.set(x, y, z);
				dummy.rotation.x = Math.PI / 2;
				dummy.updateMatrix();
				instancedMesh.setMatrixAt(i, dummy.matrix);
			}
			instancedMesh.instanceMatrix.needsUpdate = true;
			composer.render();
			requestAnimationFrame(animate);
		};

		// Force initial sizing
		renderer.setSize(window.innerWidth, window.innerHeight);
		composer.setSize(window.innerWidth, window.innerHeight);
		animate();

		const handleResize = () => {
			camera.aspect = window.innerWidth / window.innerHeight;
			camera.updateProjectionMatrix();
			renderer.setSize(window.innerWidth, window.innerHeight);
			composer.setSize(window.innerWidth, window.innerHeight);
		};
		window.addEventListener('resize', handleResize);

		return () => {
			window.removeEventListener('resize', handleResize);
			renderer.dispose();
		};
	});
</script>

<div bind:this={container} class="wave-bg"></div>

<style>
	.bg-canvas {
		position: fixed;
		top: 0;
		left: 0;
		width: 100vw;
		height: 100vh;
		z-index: -1; /* Pushes waves BEHIND everything else */
		background: transparent; 
		pointer-events: none; /* Allows you to click tabs "through" the animation */
	}
</style>