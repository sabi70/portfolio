<template>
  <div id="three-container">
    <div id="menu">
      <button id="table">TABLE</button>
      <button id="sphere">SPHERE</button>
      <button id="helix">HELIX</button>
      <button id="spiral">SPIRAL</button>
    </div>
    <div id="container" :style="customStyle"></div>
  </div>
</template>

<script lang="js">
import * as THREE from 'three';

import TWEEN from 'three/addons/libs/tween.module.js';
import { TrackballControls } from 'three/addons/controls/TrackballControls.js';
import { CSS3DRenderer, CSS3DObject } from 'three/addons/renderers/CSS3DRenderer.js';

export default {
  name: 'ThreeModel',
  data() {
    return {};
  },
  props: {
    customStyle: {
      type: Object,
      default: () => ({})
    }
  },
  mounted() {
    // MAKE SURE TO CALL IT ON MOUNTED LIFECYCLE HOOK WHEN DOM ELEMENTS ARE CREATED
    this.threeModel();
  },
  methods: {
    threeModel() {
      const containerWidth = document.getElementById('container').offsetWidth;
      const containerHeight = document.getElementById('container').offsetHeight;
      const shapes = { sphere: [], helix: [], table: [], spiral: [] };
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
      const aspectRatio = containerWidth / containerHeight;
      const groupedObject = new THREE.Group();


      init();
      animate();

      function init() {
        // CREATE CAMERA
        camera = new THREE.PerspectiveCamera(40, aspectRatio, 1, 2000);
        camera.position.z = 2000
        camera.lookAt(groupedObject.position);

        // CREATE SCENE
        scene = new THREE.Scene();
        scene.background = new THREE.Color(0x0d1117);
        
        // CREATE STACK CARDS AND ADD THEM INTO OBJECTS LIST
        createElement();

        // CREATE SIMPLE RENDERER
        renderer = new THREE.WebGLRenderer();
        renderer.setSize(containerWidth, containerHeight);
        renderer.domElement.style.position = 'absolute';
        renderer.domElement.style.top= 2;
        document.getElementById('container').appendChild(renderer.domElement);


        // CREATE cssRenderer 
        cssRenderer = new CSS3DRenderer();
        cssRenderer.setSize(containerWidth, containerHeight);
        cssRenderer.domElement.style.position = 'absolute';
        cssRenderer.domElement.style.top = 2;
        document.getElementById('container').appendChild(cssRenderer.domElement);
        

        // CREATE CONTROLLER
        controls = new TrackballControls(camera, cssRenderer.domElement);
        controls.minDistance = 750;
        controls.maxDistance = 2000;
        controls.addEventListener('change', render);

        window.addEventListener('resize', onWindowResize);

        // ====================================================================

        // SPHERE SHAPE
        const vector = new THREE.Vector3();

        for (let i = 0, l = objects.length; i < l; i++) {
          const phi = Math.acos(-1 + (2 * i) / l);
          const theta = Math.sqrt(l * Math.PI) * phi;

          const object = new THREE.Object3D();

          object.position.setFromSphericalCoords(400, phi, theta);
          vector.copy( object.position ).multiplyScalar(5);
          object.lookAt(vector);
          shapes.sphere.push(object);
        }

        // TABLE SHAPE
        for ( let i = 0; i < objects.length; i++) {
          const object = new THREE.Object3D();
          const xPos = ( (i % 4 ) * 325 ) - 500;
          const yPos = ( - ( Math.floor( i / 4 ) % 4 ) * 150 ) + 400;
          const zPos = 0;
          object.position.set(xPos, yPos, zPos);
          shapes.table.push(object);
        }

        // HELIX SHAPE
        for (let i = 0, l = objects.length; i < l; i++) {
          const theta = i * 0.42 + Math.PI;
          const y = 0;

          const object = new THREE.Object3D();
          object.position.setFromCylindricalCoords( 900, theta, y);

          vector.x = object.position.x * 2;
          vector.y = object.position.y;
          vector.z = object.position.z * 2;

          object.lookAt(vector);
          shapes.helix.push(object);
        }

        // SPIRAL SHAPE
        const spacing = 50;
        for (let i = 0; i < objects.length; i++ ) {
          const object = new THREE.Object3D();
          const angle = i * 0.5;
          const x = spacing * i * Math.cos(angle);
          const y = spacing * i * Math.sin(angle);
          const z = 200 * angle;
          object.position.set(x,y,z);
          shapes.spiral.push(object);
        }

        transform(shapes.table, 1500);

      }

      // ======================================================================

      // EVENT LISTENER ON WINDOW RESIZE
      function onWindowResize() {
        camera.aspect = containerWidth / containerHeight;
        camera.updateProjectionMatrix();
        cssRenderer.setSize(containerWidth, containerHeight);
        cssRenderer.render(scene, camera);
      }

      //       
      function animate() {        
        requestAnimationFrame(animate);
        renderer.render(scene, camera);
        cssRenderer.render(scene, camera);
        TWEEN.update();
        controls.update();
      }
      
      // STACK CARD CREATION FUNC
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
          
          groupedObject.add(cssObject);
          scene.add(cssObject);
          objects.push(cssObject);
        }
      }

      // EVENT LISTENERS FOR BUTTONS  
      const sphereButton = document.getElementById('sphere');
      sphereButton.addEventListener('click', function() {
        transform(shapes.sphere, 1500);
      });

      const tableButton = document.getElementById('table');
      tableButton.addEventListener('click', function() {
        transform(shapes.table, 1500);
      });

      const helixButton = document.getElementById('helix');
      helixButton.addEventListener('click', function() {
        transform(shapes.helix, 1500);
      });

      const spiralButton = document.getElementById('spiral');
      spiralButton.addEventListener('click', function() {
        transform(shapes.spiral, 1500);
      });

      function transform(shapes, duration) {
        TWEEN.removeAll();

        for (let i = 0; i < objects.length; i++) {
          const object = objects[ i ];
          const shape = shapes[ i ];

          new TWEEN.Tween( object.position )
            .to( { x: shape.position.x, y: shape.position.y, z: shape.position.z }, Math.random() * duration + duration)
            .easing(TWEEN.Easing.Quintic.Out)
            .start();

          new TWEEN.Tween( object.rotation )
            .to( { x: shape.rotation.x, y: shape.rotation.y, z: shape.rotation.z }, Math.random() * duration + duration)
            .easing(TWEEN.Easing.Quintic.Out)
            .start();
        }

        new TWEEN.Tween(this)
          .to( {}, duration * 2 )
          .onUpdate( render )
          .start();

      }

      function render() {
        renderer.render(scene, camera);
        cssRenderer.render(scene, camera);
      }
    }
  }
}
</script>

<style lang="css">
#three-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
#menu {
  width: 100%;
  text-align: center;
  z-index: 1;
}
    #menu button {
      color: rgba(127,255,255,0.75);
      background-color: transparent;
      outline: 1px solid rgba(127,255,255,0.75);
      border: 0px;
      padding: 8px 14px;
      margin: 5px;
      cursor: pointer;
      border-radius: 5px;
    }
    #menu button:hover {
      background-color: rgba(0,255,255,0.5);
      box-shadow: 0px 0px 10px #8ff;
    }
    #menu button:active {
      color: #000000;
      background-color: rgba(0,255,255,0.75);
      box-shadow: 0px 0px 10px #8ff;
    }


.element {
  width: 300px;
  height: 120px;
  color: #8ff;
  box-shadow: 0px 0px 12px rgba(0,255,255,0.5);
  border: 1px solid rgba(127,255,255,0.25);
  border-radius: 10px;
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