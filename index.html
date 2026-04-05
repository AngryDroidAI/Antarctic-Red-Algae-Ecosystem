<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>3D Antarctic Red Algae Ecosystem</title>
<style>
  * { margin: 0; padding: 0; box-sizing: border-box; }
  body { overflow: hidden; background: #0a0a1a; font-family: 'Segoe UI', system-ui, sans-serif; }
  canvas { display: block; }

  #ui {
    position: absolute;
    top: 15px;
    right: 15px;
    background: rgba(10, 15, 30, 0.85);
    backdrop-filter: blur(10px);
    padding: 18px;
    border-radius: 12px;
    min-width: 240px;
    color: #e0e0e0;
    border: 1px solid rgba(126, 200, 227, 0.2);
    box-shadow: 0 8px 32px rgba(0,0,0,0.4);
  }
  #ui h2 {
    font-size: 1rem;
    color: #7ec8e3;
    margin-bottom: 12px;
    text-align: center;
  }
  .control-group { margin-bottom: 12px; }
  .control-group label {
    display: flex;
    justify-content: space-between;
    font-size: 0.8rem;
    color: #aaa;
    margin-bottom: 4px;
  }
  .control-group label span { color: #7ec8e3; font-weight: bold; }
  input[type="range"] {
    width: 100%;
    accent-color: #e74c3c;
    height: 6px;
  }
  .stats {
    background: rgba(15, 52, 96, 0.6);
    padding: 10px;
    border-radius: 8px;
    font-size: 0.75rem;
    line-height: 1.8;
    margin-top: 10px;
  }
  .stats div { display: flex; justify-content: space-between; }
  .stat-label { color: #888; }
  .stat-value { color: #fff; font-weight: bold; }
  .legend {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    font-size: 0.7rem;
    margin-top: 10px;
  }
  .legend-item { display: flex; align-items: center; gap: 4px; }
  .legend-dot { width: 8px; height: 8px; border-radius: 50%; }

  button {
    width: 100%;
    background: linear-gradient(135deg, #e74c3c, #c0392b);
    color: white;
    border: none;
    padding: 8px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 0.85rem;
    margin-top: 10px;
    transition: transform 0.1s;
  }
  button:hover { transform: scale(1.02); }

  #info {
    position: absolute;
    bottom: 15px;
    left: 50%;
    transform: translateX(-50%);
    color: rgba(255,255,255,0.5);
    font-size: 0.75rem;
    text-align: center;
  }

  #loading {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    color: #7ec8e3;
    font-size: 1.2rem;
  }
</style>
</head>
<body>
<div id="loading">Loading 3D Simulation...</div>
<div id="ui">
  <h2>Antarctic Ecosystem</h2>
  <div class="control-group">
    <label>Temperature <span id="tempVal">-5°C</span></label>
    <input type="range" id="tempSlider" min="-20" max="10" value="-5" step="0.5">
  </div>
  <div class="control-group">
    <label>Sunlight <span id="sunVal">50%</span></label>
    <input type="range" id="sunSlider" min="0" max="100" value="50">
  </div>
  <div class="control-group">
    <label>Nutrients <span id="nutVal">50%</span></label>
    <input type="range" id="nutSlider" min="0" max="100" value="50">
  </div>
  <div class="stats">
    <div><span class="stat-label">Algae:</span> <span class="stat-value" id="algaePop">0</span></div>
    <div><span class="stat-label">Growth Rate:</span> <span class="stat-value" id="growthRate">0%</span></div>
    <div><span class="stat-label">Snow Albedo:</span> <span class="stat-value" id="albedo">85%</span></div>
    <div><span class="stat-label">Melt Rate:</span> <span class="stat-value" id="meltRate">0mm/day</span></div>
    <div><span class="stat-label">CO₂ Absorbed:</span> <span class="stat-value" id="co2">0 kg</span></div>
  </div>
  <div class="legend">
    <div class="legend-item"><span class="legend-dot" style="background:#e74c3c"></span> Red Algae</div>
    <div class="legend-item"><span class="legend-dot" style="background:#2ecc71"></span> Green Algae</div>
    <div class="legend-item"><span class="legend-dot" style="background:#f39c12"></span> Bacteria</div>
    <div class="legend-item"><span class="legend-dot" style="background:#3498db"></span> Krill</div>
  </div>
  <button id="resetBtn">Reset</button>
</div>
<div id="info">Click & drag to rotate · Scroll to zoom · Right-click to pan</div>
<script type="importmap">
{
  "imports": {
    "three": "https://cdn.jsdelivr.net/npm/three@0.160.0/build/three.module.js",
    "three/addons/": "https://cdn.jsdelivr.net/npm/three@0.160.0/examples/jsm/"
  }
}
</script>
<script type="module">
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
let scene, camera, renderer, controls;
let snowTerrain, waterPlane, sunLight, ambientLight;
let temperature = -5, sunlight = 50, nutrients = 50;
let time = 0, totalCO2 = 0;
const organisms = [];
const organismMeshes = [];
const config = {
  terrainSize: 100,
  terrainSegments: 128,
  maxOrganisms: 400,
  spawnRate: 0.3
};
function init() {
  scene = new THREE.Scene();
  scene.fog = new THREE.FogExp2(0x8899aa, 0.008);
  camera = new THREE.PerspectiveCamera(60, window.innerWidth / window.innerHeight, 0.1, 500);
  camera.position.set(30, 35, 50);
  renderer = new THREE.WebGLRenderer({ antialias: true, alpha: true });
  renderer.setSize(window.innerWidth, window.innerHeight);
  renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
  renderer.shadowMap.enabled = true;
  renderer.shadowMap.type = THREE.PCFSoftShadowMap;
  renderer.toneMapping = THREE.ACESFilmicToneMapping;
  renderer.toneMappingExposure = 1.2;
  document.body.appendChild(renderer.domElement);
  controls = new OrbitControls(camera, renderer.domElement);
  controls.enableDamping = true;
  controls.dampingFactor = 0.05;
  controls.maxPolarAngle = Math.PI / 2.1;
  controls.minDistance = 15;
  controls.maxDistance = 120;
  controls.target.set(0, 0, 0);
  createLighting();
  createSky();
  createSnowTerrain();
  createWater();
  createSnowParticles();
  createMountains();
  window.addEventListener('resize', onResize);
  document.getElementById('loading').style.display = 'none';
  setupUI();
  animate();
}
function createLighting() {
  ambientLight = new THREE.AmbientLight(0x4466aa, 0.6);
  scene.add(ambientLight);
  sunLight = new THREE.DirectionalLight(0xffeedd, 1);
  sunLight.position.set(50, 80, 30);
  sunLight.castShadow = true;
  sunLight.shadow.mapSize.set(2048, 2048);
  sunLight.shadow.camera.left = -60;
  sunLight.shadow.camera.right = 60;
  sunLight.shadow.camera.top = 60;
  sunLight.shadow.camera.bottom = -60;
  scene.add(sunLight);
  const hemiLight = new THREE.HemisphereLight(0x88aacc, 0x444466, 0.4);
  scene.add(hemiLight);
  const sunGeo = new THREE.SphereGeometry(3, 32, 32);
  const sunMat = new THREE.MeshBasicMaterial({ color: 0xffffcc });
  const sunMesh = new THREE.Mesh(sunGeo, sunMat);
  sunMesh.position.copy(sunLight.position).normalize().multiplyScalar(200);
  scene.add(sunMesh);
}
function createSky() {
  const skyGeo = new THREE.SphereGeometry(200, 32, 32);
  const skyMat = new THREE.ShaderMaterial({
    uniforms: {
      topColor: { value: new THREE.Color(0x1a2a4a) },
      bottomColor: { value: new THREE.Color(0x6688aa) },
      offset: { value: 20 },
      exponent: { value: 0.4 }
    },
    vertexShader: `
      varying vec3 vWorldPosition;
      void main() {
        vec4 worldPosition = modelMatrix * vec4(position, 1.0);
        vWorldPosition = worldPosition.xyz;
        gl_Position = projectionMatrix * modelViewMatrix * vec4(position, 1.0);
      }
    `,
    fragmentShader: `
      uniform vec3 topColor;
      uniform vec3 bottomColor;
      uniform float offset;
      uniform float exponent;
      varying vec3 vWorldPosition;
      void main() {
        float h = normalize(vWorldPosition + offset).y;
        gl_FragColor = vec4(mix(bottomColor, topColor, max(pow(max(h, 0.0), exponent), 0.0)), 1.0);
      }
    `,
    side: THREE.BackSide
  });
  scene.add(new THREE.Mesh(skyGeo, skyMat));
}
function createSnowTerrain() {
  const geo = new THREE.PlaneGeometry(
    config.terrainSize, config.terrainSize,
    config.terrainSegments, config.terrainSegments
  );
  geo.rotateX(-Math.PI / 2);
  const positions = geo.attributes.position;
  for (let i = 0; i < positions.count; i++) {
    const x = positions.getX(i);
    const z = positions.getZ(i);
    const y = getTerrainHeight(x, z);
    positions.setY(i, y);
  }
  geo.computeVertexNormals();
  const mat = new THREE.MeshStandardMaterial({
    color: 0xf0f5fa,
    roughness: 0.8,
    metalness: 0.1,
    flatShading: false
  });
  snowTerrain = new THREE.Mesh(geo, mat);
  snowTerrain.receiveShadow = true;
  snowTerrain.castShadow = true;
  scene.add(snowTerrain);
}
function getTerrainHeight(x, z) {
  let y = 0;
  y += Math.sin(x * 0.05) * Math.cos(z * 0.05) * 3;
  y += Math.sin(x * 0.1 + 1) * Math.cos(z * 0.08 + 2) * 1.5;
  y += Math.sin(x * 0.2 + z * 0.15) * 0.5;
  return y;
}
function createWater() {
  const geo = new THREE.PlaneGeometry(200, 200, 64, 64);
  geo.rotateX(-Math.PI / 2);
  const mat = new THREE.ShaderMaterial({
    uniforms: {
      uTime: { value: 0 },
      uColor: { value: new THREE.Color(0x1a5276) },
      uOpacity: { value: 0.6 }
    },
    vertexShader: `
      uniform float uTime;
      varying vec2 vUv;
      varying float vWave;
      void main() {
        vUv = uv;
        vec3 pos = position;
        float wave = sin(pos.x * 0.3 + uTime) * 0.3 + sin(pos.z * 0.5 + uTime * 1.3) * 0.2;
        pos.y += wave;
        vWave = wave;
        gl_Position = projectionMatrix * modelViewMatrix * vec4(pos, 1.0);
      }
    `,
    fragmentShader: `
      uniform vec3 uColor;
      uniform float uOpacity;
      uniform float uTime;
      varying vec2 vUv;
      varying float vWave;
      void main() {
        float foam = smoothstep(0.4, 0.5, vWave) * 0.3;
        vec3 color = uColor + vec3(foam);
        gl_FragColor = vec4(color, uOpacity);
      }
    `,
    transparent: true,
    side: THREE.DoubleSide
  });
  waterPlane = new THREE.Mesh(geo, mat);
  waterPlane.position.y = -2;
  scene.add(waterPlane);
}
function createSnowParticles() {
  const count = 2000;
  const geo = new THREE.BufferGeometry();
  const positions = new Float32Array(count * 3);
  const velocities = new Float32Array(count * 3);
  for (let i = 0; i < count; i++) {
    positions[i * 3] = (Math.random() - 0.5) * 100;
    positions[i * 3 + 1] = Math.random() * 40;
    positions[i * 3 + 2] = (Math.random() - 0.5) * 100;
    velocities[i * 3] = (Math.random() - 0.5) * 0.1;
    velocities[i * 3 + 1] = -0.05 - Math.random() * 0.1;
    velocities[i * 3 + 2] = (Math.random() - 0.5) * 0.1;
  }
  geo.setAttribute('position', new THREE.BufferAttribute(positions, 3));
  geo.setAttribute('velocity', new THREE.BufferAttribute(velocities, 3));
  const mat = new THREE.PointsMaterial({
    color: 0xffffff,
    size: 0.3,
    transparent: true,
    opacity: 0.6,
    sizeAttenuation: true
  });
  const particles = new THREE.Points(geo, mat);
  particles.userData.velocities = velocities;
  scene.add(particles);
  return particles;
}
function createMountains() {
  const mountainPositions = [
    { x: -60, z: -50, s: 25, h: 35 },
    { x: -40, z: -60, s: 20, h: 28 },
    { x: 50, z: -55, s: 30, h: 40 },
    { x: 70, z: -45, s: 22, h: 32 },
    { x: -70, z: -40, s: 18, h: 25 },
    { x: 0, z: -70, s: 35, h: 45 },
    { x: -30, z: 50, s: 20, h: 22 },
    { x: 40, z: 55, s: 25, h: 28 }
  ];
  mountainPositions.forEach(m => {
    const geo = new THREE.ConeGeometry(m.s, m.h, 6, 4);
    const mat = new THREE.MeshStandardMaterial({
      color: 0xddeeff,
      roughness: 0.9,
      flatShading: true
    });
    const mountain = new THREE.Mesh(geo, mat);
    mountain.position.set(m.x, m.h / 2 - 2, m.z);
    mountain.castShadow = true;
    mountain.receiveShadow = true;
    scene.add(mountain);
    const snowCapGeo = new THREE.ConeGeometry(m.s * 0.4, m.h * 0.3, 6, 2);
    const snowCapMat = new THREE.MeshStandardMaterial({
      color: 0xffffff,
      roughness: 0.7,
      flatShading: true
    });
    const snowCap = new THREE.Mesh(snowCapGeo, snowCapMat);
    snowCap.position.set(m.x, m.h * 0.85 - 2, m.z);
    scene.add(snowCap);
  });
}
function getGrowthRate() {
  const tempFactor = temperature > -10 && temperature < 5
    ? 1 - Math.abs(temperature + 2) / 8
    : 0;
  return Math.max(0, tempFactor * (sunlight / 100) * (nutrients / 100));
}
function getAlbedo() {
  const redCount = organisms.filter(o => o.type === 'red').length;
  return Math.max(30, 85 - Math.min(40, redCount * 0.05));
}
function getMeltRate() {
  const albedo = getAlbedo();
  const baseMelt = Math.max(0, temperature + 5) * 2;
  return baseMelt * (1 + (100 - albedo) / 100 * 2);
}
function createOrganismMesh(type) {
  let geo, mat;
  const colors = {
    red: 0xe74c3c,
    green: 0x2ecc71,
    bacteria: 0xf39c12,
    krill: 0x3498db
  };
  if (type === 'krill') {
    geo = new THREE.CapsuleGeometry(0.3, 0.8, 4, 8);
    mat = new THREE.MeshStandardMaterial({
      color: colors[type],
      emissive: colors[type],
      emissiveIntensity: 0.2,
      roughness: 0.4,
      metalness: 0.3
    });
  } else {
    geo = new THREE.SphereGeometry(0.25 + Math.random() * 0.2, 8, 8);
    mat = new THREE.MeshStandardMaterial({
      color: colors[type],
      emissive: colors[type],
      emissiveIntensity: 0.3,
      roughness: 0.6,
      transparent: true,
      opacity: 0.85
    });
  }
  const mesh = new THREE.Mesh(geo, mat);
  mesh.castShadow = true;
  return mesh;
}
function spawnOrganism() {
  if (organisms.length >= config.maxOrganisms) return;
  const growthRate = getGrowthRate();
  if (Math.random() > growthRate * config.spawnRate) return;
  const types = ['red', 'red', 'red', 'green', 'bacteria'];
  const type = types[Math.floor(Math.random() * types.length)];
  const angle = Math.random() * Math.PI * 2;
  const radius = Math.random() * 35;
  const x = Math.cos(angle) * radius;
  const z = Math.sin(angle) * radius;
  const y = getTerrainHeight(x, z) + 0.5 + Math.random() * 2;
  const organism = {
    type,
    x, y, z,
    vx: (Math.random() - 0.5) * 0.05,
    vy: (Math.random() - 0.5) * 0.02,
    vz: (Math.random() - 0.5) * 0.05,
    age: 0,
    maxAge: 600 + Math.random() * 1200,
    alive: true,
    phase: Math.random() * Math.PI * 2
  };
  const mesh = createOrganismMesh(type);
  mesh.position.set(x, y, z);
  scene.add(mesh);
  organisms.push(organism);
  organismMeshes.push(mesh);
}
function updateOrganisms() {
  const growthRate = getGrowthRate();
  const maxPop = 350 * growthRate * (nutrients / 50);
  for (let i = organisms.length - 1; i >= 0; i--) {
    const org = organisms[i];
    const mesh = organismMeshes[i];
    org.age++;
    org.phase += 0.03;
    if (org.age > org.maxAge) {
      scene.remove(mesh);
      mesh.geometry.dispose();
      mesh.material.dispose();
      organisms.splice(i, 1);
      organismMeshes.splice(i, 1);
      continue;
    }
    const speedMult = temperature > -5 ? 1 : 0.2;
    org.x += org.vx * speedMult;
    org.y += Math.sin(org.phase) * 0.02;
    org.z += org.vz * speedMult;
    const terrainY = getTerrainHeight(org.x, org.z);
    org.y = Math.max(terrainY + 0.5, org.y);
    org.x = THREE.MathUtils.clamp(org.x, -45, 45);
    org.z = THREE.MathUtils.clamp(org.z, -45, 45);
    mesh.position.set(org.x, org.y, org.z);
    mesh.rotation.y += 0.02;
    const pulse = 1 + Math.sin(org.phase * 2) * 0.1;
    mesh.scale.setScalar(pulse);
    if (org.type === 'krill') {
      mesh.lookAt(org.x + org.vx, org.y, org.z + org.vz);
    }
  }
  if (organisms.length < maxPop) {
    for (let i = 0; i < 3; i++) spawnOrganism();
  }
  if (temperature > 0 && organisms.filter(o => o.type === 'krill').length < 20) {
    if (Math.random() < 0.02) {
      const angle = Math.random() * Math.PI * 2;
      const radius = Math.random() * 30;
      const x = Math.cos(angle) * radius;
      const z = Math.sin(angle) * radius;
      const y = Math.max(getTerrainHeight(x, z), -1) + 1;
      const org = {
        type: 'krill', x, y, z,
        vx: (Math.random() - 0.5) * 0.1,
        vy: 0,
        vz: (Math.random() - 0.5) * 0.1,
        age: 0, maxAge: 1500 + Math.random() * 1000,
        alive: true, phase: Math.random() * Math.PI * 2
      };
      const mesh = createOrganismMesh('krill');
      mesh.position.set(x, y, z);
      scene.add(mesh);
      organisms.push(org);
      organismMeshes.push(mesh);
    }
  }
}
function updateEnvironment() {
  const sunIntensity = sunlight / 100;
  sunLight.intensity = sunIntensity * 2;
  ambientLight.intensity = 0.3 + sunIntensity * 0.5;
  const snowLevel = Math.max(0, Math.min(1, (10 - temperature) / 15));
  waterPlane.position.y = -2 + (1 - snowLevel) * 4;
  waterPlane.material.uniforms.uOpacity.value = 0.4 + (1 - snowLevel) * 0.3;
  const redCount = organisms.filter(o => o.type === 'red').length;
  const redness = Math.min(1, redCount / 150);
  const r = Math.floor(240 - redness * 150);
  const g = Math.floor(245 - redness * 180);
  const b = Math.floor(250 - redness * 180);
  snowTerrain.material.color.setRGB(r / 255, g / 255, b / 255);
  const skyTop = new THREE.Color().setHSL(0.6, 0.4, 0.1 + sunIntensity * 0.3);
  const skyBottom = new THREE.Color().setHSL(0.55, 0.3, 0.3 + sunIntensity * 0.4);
  scene.children.forEach(child => {
    if (child.material && child.material.uniforms && child.material.uniforms.topColor) {
      child.material.uniforms.topColor.value.copy(skyTop);
      child.material.uniforms.bottomColor.value.copy(skyBottom);
    }
  });
  const fogDensity = 0.005 + (1 - sunIntensity) * 0.01;
  scene.fog.density = fogDensity;
}
function updateSnowParticles(particles) {
  const positions = particles.geometry.attributes.position.array;
  const velocities = particles.userData.velocities;
  const snowLevel = Math.max(0, Math.min(1, (10 - temperature) / 15));
  particles.material.opacity = snowLevel * 0.6;
  for (let i = 0; i < positions.length / 3; i++) {
    positions[i * 3] += velocities[i * 3];
    positions[i * 3 + 1] += velocities[i * 3 + 1];
    positions[i * 3 + 2] += velocities[i * 3 + 2];
    if (positions[i * 3 + 1] < getTerrainHeight(positions[i * 3], positions[i * 3 + 2])) {
      positions[i * 3] = (Math.random() - 0.5) * 100;
      positions[i * 3 + 1] = 35 + Math.random() * 10;
      positions[i * 3 + 2] = (Math.random() - 0.5) * 100;
    }
  }
  particles.geometry.attributes.position.needsUpdate = true;
}
function updateStats() {
  const algaeCount = organisms.filter(o => o.type === 'red').length;
  const growthRate = getGrowthRate() * 100;
  const albedo = getAlbedo();
  const meltRate = getMeltRate();
  document.getElementById('algaePop').textContent = algaeCount;
  document.getElementById('growthRate').textContent = growthRate.toFixed(1) + '%';
  document.getElementById('albedo').textContent = albedo.toFixed(0) + '%';
  document.getElementById('meltRate').textContent = meltRate.toFixed(1) + 'mm/day';
  document.getElementById('co2').textContent = totalCO2.toFixed(2) + ' kg';
}
function setupUI() {
  document.getElementById('tempSlider').addEventListener('input', e => {
    temperature = parseFloat(e.target.value);
    document.getElementById('tempVal').textContent = temperature + '°C';
  });
  document.getElementById('sunSlider').addEventListener('input', e => {
    sunlight = parseInt(e.target.value);
    document.getElementById('sunVal').textContent = sunlight + '%';
  });
  document.getElementById('nutSlider').addEventListener('input', e => {
    nutrients = parseInt(e.target.value);
    document.getElementById('nutVal').textContent = nutrients + '%';
  });
  document.getElementById('resetBtn').addEventListener('click', () => {
    organismMeshes.forEach(m => {
      scene.remove(m);
      m.geometry.dispose();
      m.material.dispose();
    });
    organisms.length = 0;
    organismMeshes.length = 0;
    totalCO2 = 0;
    time = 0;
    temperature = -5;
    sunlight = 50;
    nutrients = 50;
    document.getElementById('tempSlider').value = -5;
    document.getElementById('sunSlider').value = 50;
    document.getElementById('nutSlider').value = 50;
    document.getElementById('tempVal').textContent = '-5°C';
    document.getElementById('sunVal').textContent = '50%';
    document.getElementById('nutVal').textContent = '50%';
  });
}
function onResize() {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
}
function animate() {
  requestAnimationFrame(animate);
  time++;
  controls.update();
  const snowParticles = scene.children.find(c => c.type === 'Points');
  if (snowParticles) updateSnowParticles(snowParticles);
  waterPlane.material.uniforms.uTime.value = time * 0.02;
  updateOrganisms();
  updateEnvironment();
  if (time % 30 === 0) {
    totalCO2 += organisms.filter(o => o.type === 'red').length * 0.00005;
  }
  updateStats();
  renderer.render(scene, camera);
}
init();
</script>
</body>
</html>
