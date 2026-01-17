<template>
  <div class="canvas_for_three" ref="threeContainer"></div>
</template>

<script>
import * as THREE from "three";

import pythonTexture from "~/assets/images/python.webp";
import javascriptTexture from "~/assets/images/javascript.png";
import golangTexture from "~/assets/images/golang.png";
import argocdTexture from "~/assets/images/argocd.png";
import k8sTexture from "~/assets/images/k8s.png";
import tfTexture from "~/assets/images/tf.png";
import awsTexture from "~/assets/images/aws.png";
import sparkTexture from "~/assets/images/spark.png";

export default {
  name: "TechSolarSystem",

  data() {
    return {
      scene: null,
      camera: null,
      renderer: null,
      orbitObjects: [],
      orbitGroup: null,
      raycaster: new THREE.Raycaster(),
      mouse: new THREE.Vector2(),
      animationId: null,
    };
  },

  mounted() {
    this.initScene();
    this.animate();
    window.addEventListener("resize", this.onResize);
    window.addEventListener("mousemove", this.onMouseMove);
    window.addEventListener("click", this.onClick);
  },

  beforeUnmount() {
    cancelAnimationFrame(this.animationId);
    window.removeEventListener("resize", this.onResize);
    window.removeEventListener("mousemove", this.onMouseMove);
    window.removeEventListener("click", this.onClick);
  },

  methods: {
    initScene() {
      const container = this.$refs.threeContainer;

      // Scene
      this.scene = new THREE.Scene();
      this.scene.background = new THREE.Color(0x0d0d0d);

      // Camera
      this.camera = new THREE.PerspectiveCamera(
        70,
        container.clientWidth / container.clientHeight,
        1,
        5000
      );
      this.camera.position.set(0, 0, 900);

      // Renderer
      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setSize(container.clientWidth, container.clientHeight);
      this.renderer.setPixelRatio(window.devicePixelRatio);
      container.appendChild(this.renderer.domElement);

      // Lights
      this.scene.add(new THREE.AmbientLight(0xffffff, 0.6));

      const sunLight = new THREE.PointLight(0xffaa33, 2, 2000);
      sunLight.position.set(0, 0, 0);
      this.scene.add(sunLight);

      // ☀️ Sun (center)
      const sun = new THREE.Mesh(
        new THREE.SphereGeometry(120, 64, 64),
        new THREE.MeshStandardMaterial({
          color: 0xffaa33,
          emissive: 0xff6600,
          emissiveIntensity: 1.2,
          roughness: 0.4,
          metalness: 0.1,
        })
      );
      this.scene.add(sun);

      // Orbit group (flat, no tilt)
      this.orbitGroup = new THREE.Group();
      this.scene.add(this.orbitGroup);

      // Orbiting cubes
      const loader = new THREE.TextureLoader();

      const textures = [
        loader.load(pythonTexture),
        loader.load(tfTexture),
        loader.load(javascriptTexture),
        loader.load(sparkTexture),
        loader.load(golangTexture),
        loader.load(argocdTexture),
        loader.load(awsTexture),
        loader.load(k8sTexture),
      ];

      const radius = 450;
      const orbitSpeed = 0.003;

      const angleStep = (Math.PI * 2) / textures.length;

      textures.forEach((texture, index) => {
        const cube = new THREE.Mesh(
          new THREE.BoxGeometry(120, 120, 120),
          new THREE.MeshStandardMaterial({
            map: texture,
            roughness: 0.8,
            metalness: 0.2,
          })
        );

        cube.userData = {
          angle: index * angleStep,
          speed: orbitSpeed,
          radius,
        };

        this.orbitObjects.push(cube);
        this.orbitGroup.add(cube);
      });
    },

    animate() {
      this.animationId = requestAnimationFrame(this.animate);

      // Update orbiting cubes
      this.orbitObjects.forEach((cube) => {
        cube.userData.angle += cube.userData.speed;

        cube.position.set(
          Math.cos(cube.userData.angle) * cube.userData.radius,
          Math.sin(cube.userData.angle) * cube.userData.radius,
          0
        );

        cube.rotation.x += 0.01;
        cube.rotation.y += 0.01;
      });

      this.renderer.render(this.scene, this.camera);
    },

    onResize() {
      const container = this.$refs.threeContainer;
      this.camera.aspect = container.clientWidth / container.clientHeight;
      this.camera.updateProjectionMatrix();
      this.renderer.setSize(container.clientWidth, container.clientHeight);
    },

    onMouseMove(event) {
      this.mouse.x = (event.clientX / window.innerWidth) * 2 - 1;
      this.mouse.y = -(event.clientY / window.innerHeight) * 2 + 1;
    },

    onClick() {
      this.raycaster.setFromCamera(this.mouse, this.camera);
      const intersects = this.raycaster.intersectObjects(this.orbitObjects);

      if (intersects.length > 0) {
        console.log("Clicked:", intersects[0].object);
      }
    },
  },
};
</script>

<style scoped>
.canvas_for_three {
  width: 100%;
  height: 100vh;
  position: relative;
}
</style>
