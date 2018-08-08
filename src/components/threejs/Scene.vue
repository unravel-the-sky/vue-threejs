<template>
    <div>
        lol:
        <div id="threejs-content">
        </div>
    </div>
</template>

<style scoped>
</style>

<script>
import * as THREE from "three";
const scene = new THREE.Scene();

export default {
  name: "scene",
  data() {
    return {
      camera: null,
      renderer: null,
      geometry: null,
      material: null,
      mesh: null,
      height: 300,
      width: 500
    };
  },
  created() {},
  mounted() {
      this.init();
      this.animate();
  },
  methods: {
    init() {
      this.camera = new THREE.PerspectiveCamera(70, this.width / this.height, 0.01, 1000);
      this.camera.position.z = 100;

      this.geometry = new THREE.BoxGeometry(50, 10, 50);
      this.material = new THREE.MeshNormalMaterial();

      this.mesh = new THREE.Mesh(this.geometry, this.material);
      scene.add(this.mesh);

      this.renderer = new THREE.WebGLRenderer({ antialias: true });
      this.renderer.setSize(this.width, this.height);
      
      const content = document.getElementById('threejs-content');
      content.appendChild(this.renderer.domElement)
    //   document.body.appendChild(this.renderer.domElement);
    },
    addParticles(){
        // add particles here
    },
    animate(){
        requestAnimationFrame(this.animate)

        this.mesh.rotation.x += 0.01;
        this.mesh.rotation.y += 0.02;
        this.mesh.rotation.z += 0.01;

        this.renderer.render(scene, this.camera)
    }
  }
};
</script>
