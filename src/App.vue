<template>
  <div id="app">
    <canvas id="example"></canvas>
  </div>
</template>

<script>
import * as THREE from "three";
import { ObjectControls, CameraControls } from "threejs-object-controls";

export default {
  name: "App",
  components: {},
  mounted() {
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
    );

    const renderer = new THREE.WebGLRenderer({
      canvas: document.getElementById("example"),
    });
    renderer.setSize(window.innerWidth, window.innerHeight);

    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);

    const geometry2 = new THREE.PlaneGeometry(5, 5);
    const material2 = new THREE.MeshBasicMaterial({ color: 0xffffff });
    const plane = new THREE.Mesh(geometry2, material2);
    scene.add(plane);

    plane.position.z = -2;

    camera.position.z = 5;

    const cameraControl = new CameraControls(camera, renderer.domElement);
    cameraControl.setEnableRotate(false);

    const objControl = new ObjectControls(cube, 2, camera, renderer.domElement);

    function animate() {
      requestAnimationFrame(animate);
      cameraControl.update();
      objControl.update();
      renderer.render(scene, camera);
    }
    animate();
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
