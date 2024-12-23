<template>
    <div ref="canvasContainer" class="canvas-container"></div>
  </template>
  
  <script setup>
  import { onMounted, ref } from 'vue';
  import * as THREE from 'three';
  
  const canvasContainer = ref(null);
  
  onMounted(() => {
    // 创建场景、相机、渲染器
    const scene = new THREE.Scene();
    const camera = new THREE.PerspectiveCamera(75, window.innerWidth / window.innerHeight, 0.1, 1000);
    const renderer = new THREE.WebGLRenderer();
    renderer.setSize(window.innerWidth, window.innerHeight);
    canvasContainer.value.appendChild(renderer.domElement);
  
    // 创建一个立方体
    const geometry = new THREE.BoxGeometry();
    const material = new THREE.MeshBasicMaterial({ color: 0x00ff00 });
    const cube = new THREE.Mesh(geometry, material);
    scene.add(cube);
  
    camera.position.z = 5;
  
    // 动画函数
    const animate = function () {
      requestAnimationFrame(animate);
  
      cube.rotation.x += 0.01;
      cube.rotation.y += 0.01;
  
      renderer.render(scene, camera);
    };
  
    animate();
  });
  </script>
  
  <style scoped>
  .canvas-container {
    width: 100%;
    height: 100vh;
    margin: 0;
    padding: 0;
  }
  </style>
  