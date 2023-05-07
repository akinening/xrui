a<template>
  <p class="note">ⓘ 画面を左右にドラッグしてみよう</p>
  <a class="btn" href="https://akinen.com">Akinen.com</a>
  <NuxtLink to="xr" class="btn btn__left">◀</NuxtLink>
  <div ref="threeContainer" class="three-container"></div>
</template>

<script>
import * as THREE from 'three';
import { OrbitControls } from 'three/examples/jsm/controls/OrbitControls.js';
import bgImg from '/assets/image/About.jpg'

export default {
  data() {
    return {
    };
  },
  mounted() {
    this.initThree();
  },
  methods: {
    initThree() {
      const container = this.$refs.threeContainer;

      const renderer = new THREE.WebGLRenderer();
      renderer.outputEncoding = THREE.LinearEncoding;
      renderer.setSize(container.clientWidth, container.clientHeight);
      container.appendChild(renderer.domElement);

      const fov = 75;
      const aspect = container.clientWidth / container.clientHeight;
      const near = 0.1;
      const far = 1000;
      const camera = new THREE.PerspectiveCamera(fov, aspect, near, far);
      camera.position.z = 1;

      const scene = new THREE.Scene();

      const sphereGeometry = new THREE.SphereGeometry(5, 32, 32);

      const loader = new THREE.TextureLoader();
      const texture = loader.load(bgImg);

      const material = new THREE.MeshBasicMaterial({
        map: texture,
        side: THREE.BackSide,
      });

      const sphere = new THREE.Mesh(sphereGeometry, material);
      scene.add(sphere);

      const controls = new OrbitControls(camera, renderer.domElement);
      controls.enableDamping = true;
      controls.enableZoom = false;
      controls.dampingFactor = 0.1;
      controls.rotateSpeed = 0.25;

      const animate = () => {
        requestAnimationFrame(animate);
        controls.update();
        renderer.render(scene, camera);
      };

      animate();
    }
  }}

</script>

<style scoped>
.three-container {
  width: 100%;
  height: 100vh;
  overflow: hidden;
}

.note {
    color: #333;
    position: absolute;
    left: calc(50% - 160px);
    text-align: center;
    width: 320px;
    padding: 4px 16px;
    border-radius: 99px;
    background-color: #fff5;
    backdrop-filter: blur(8px);
}
.btn {
    position: absolute;
    bottom: 16px;
    left: calc(50% - 80px);
    text-decoration: none;
    text-align: center;
    width: 160px;
    padding: 16px;
    border-radius: 99px;
    background-color: #fff5;
    backdrop-filter: blur(8px);
    color: #333;
    font-weight: bold;
}

.btn__left {
  left: 16px;
}

.btn__right {
  left: auto;
  right: 16px;
}
.btn:hover {
    color: #ff5894;
    transition: 0.25s 
}
</style>
