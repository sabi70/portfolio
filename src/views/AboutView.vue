<template>
  <div id="container"></div>
</template>
<script>
import * as THREE from 'three';


import { TrackballControls } from 'three/addons/controls/TrackballControls.js';
import { CSS3DRenderer, CSS3DObject } from 'three/addons/renderers/CSS3DRenderer.js';


export default {
  data() {
    return {}
  },
  mounted() {
    // MAKE SURE TO CALL IT ON MOUNTED LIFECYCLE HOOK WHEN DOM ELEMENTS ARE CREATED
    this.threeModel();
  },
  methods: {
    threeModel() {
      const stack = [
        'HTML', 24,
        'CSS', 24,
        'JavaScript', '3',
        'Vue', '5',
        'Vuetify', '4',
        'Figma', '1',
        'GIMP', '1',
        'Nginx', '1',
        'Python', '36',
        'Django', '6',
        'Gunicorn', '1',
        'Postman', '4',
        'Docker', '1',
        'Linux', '36',
        'Git', '12',
      ];
      let camera, scene, renderer;
      let cssRenderer;
      let controls;

      const objects = [];
      const aspectRatio = window.innerWidth / window.innerHeight;


      init();
      animate();

      function init() {
        // CREATE CAMERA
        camera = new THREE.PerspectiveCamera(40, aspectRatio, 1, 10000);
        camera.position.z = 3000

        // CREATE SCENE
        scene = new THREE.Scene();
        scene.background = new THREE.Color(0x000000);
        
        createElement();

        for ( let i = 0; i < objects.length; i++) {
          scene.add(objects[i]);
        }
        

        // CREATE SIMPLE RENDERER
        renderer = new THREE.WebGLRenderer();
        renderer.setSize(window.innerWidth, window.innerHeight - 100);
        renderer.domElement.style.position = 'absolute';
        renderer.domElement.style.bottom = 0;
        document.getElementById('container').appendChild(renderer.domElement);


        // CREATE cssRenderer 
        cssRenderer = new CSS3DRenderer();
        cssRenderer.setSize(window.innerWidth, window.innerHeight - 100);
        cssRenderer.domElement.style.position = 'absolute';
        cssRenderer.domElement.style.bottom = 0;
        document.getElementById('container').appendChild(cssRenderer.domElement);
        

        // CREATE CONTROLLER
        controls = new TrackballControls(camera, cssRenderer.domElement);
        controls.minDistance = 500;
        controls.maxDistance = 6000;

        window.addEventListener('resize', onWindowResize);
      }

      // EVENT LISTENER ON WINDOW RESIZE
      function onWindowResize() {
        camera.aspect = window.innerWidth / window.innerHeight;
        camera.updateProjectionMatrix();
        cssRenderer.setSize(window.innerWidth, window.innerHeight);
        cssRenderer.render(scene, camera);
      }

      // 
      function animate() {
        requestAnimationFrame(animate);
        renderer.render(scene, camera);
        cssRenderer.render(scene, camera);
        controls.update();
      }
      
      // 
      function createElement() {
        for ( let i = 0; i < stack.length; i += 2 ) {
          const element = document.createElement('div');
          element.className = 'element';
          element.style.backgroundColor = 'rgba(0,127,127,' + ( Math.random() * 0.5 + 0.25 ) + ')';

          const title = document.createElement('div');
          title.className = 'title';
          title.textContent = stack[ i ];
          element.appendChild(title);

          const period = document.createElement('div');
          period.className = 'period';
          const roundedYear = Number((stack[ i + 1 ] / 12).toFixed(1));
          period.textContent = 'Period Of Study: ' + roundedYear + ' Years';
          element.appendChild(period);

          const cssObject = new CSS3DObject(element);
          cssObject.position.x = Math.random() * 2000 - 1200;
          cssObject.position.y = Math.random() * 2000 - 1200;
          cssObject.position.z = Math.random() * 2000 - 1200;
          objects.push(cssObject);
        }
      } 
    }
  }
}
</script>
<style>
.element {
  width: 300px;
  height: 120px;
  color: #8ff;
  box-shadow: 0px 0px 12px rgba(0,255,255,0.5);
  border: 1px solid rgba(127,255,255,0.25);
  font-family: Helvetica, sans-serif;
  text-align: center;
  line-height: normal;
  cursor: default;
}
.element .title {
  position: absolute;
  top: 15px;
  left: 0px;
  right: 0px;
  font-size: 60px;
  font-weight: bold;
  color: rgba(255,255,255,0.75);
  text-shadow: 0 0 10px rgba(0,255,255,0.95);
}
.element .period {
  position: absolute;
  bottom: 15px;
  left: 0px;
  right: 0px;
  font-size: 12px;
  color: rgba(127,255,255,0.75);
}
</style>