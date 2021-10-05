<template>
  <div class="three"></div>
</template>

<script>
import * as THREE from "three";
import { OrbitControls } from "three/examples/jsm/controls/OrbitControls";
import { FontLoader } from "three/examples/jsm/loaders/FontLoader";

const MESSAGE = "He Jin Lin";
const COLOR = 0x006699;

let scene = new THREE.Scene();
let camera = new THREE.PerspectiveCamera(
  45,
  window.innerWidth / window.innerHeight,
  1,
  10000
);
let renderer = new THREE.WebGLRenderer({ antialias: true });

init();
animate();

function init() {
  const matLite = new THREE.MeshBasicMaterial({
    color: COLOR,
    transparent: true,
    opacity: 0.2,
    side: THREE.DoubleSide,
  });

  camera.position.set(0, -200, 600);
  scene.background = new THREE.Color(0xf0f0f0);
  const loader = new FontLoader();
  loader.load("fonts/helvetiker_regular.typeface.json", function onLoad(font) {
    const shapes = font.generateShapes(MESSAGE, 100);
    const geometry = new THREE.ShapeGeometry(shapes);
    geometry.computeBoundingBox();
    const xMid =
      -0.5 * (geometry.boundingBox.max.x - geometry.boundingBox.min.x);
    geometry.translate(xMid, 0, 0);

    const liteText = new THREE.Mesh(geometry, matLite);
    liteText.position.z -= 150;
    scene.add(liteText);
  });

  renderer.setPixelRatio(window.devicePixelRatio);
  renderer.setSize(window.innerWidth, window.innerHeight);
  document.body.appendChild(renderer.domElement);

  const controls = new OrbitControls(camera, renderer.domElement);
  controls.target.set(0, 0, 0);
  controls.update();
  window.addEventListener("resize", onWindowResize);
}

function onWindowResize() {
  camera.aspect = window.innerWidth / window.innerHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(window.innerWidth, window.innerHeight);
}

function animate() {
  requestAnimationFrame(animate);
  renderer.render(scene, camera);
}

export default {
  name: "ThreeView",
  data() {
    return {};
  },
  methods: {},
  computed: {},
};
</script>

<style scoped>
</style>
