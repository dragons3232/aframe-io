<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <HelloWorld msg="Welcome to Your Vue.js App"/>
  <a-scene>
    <a-assets>
      <img id="netpower" src="netpower.png">
    </a-assets>
    <a-camera
     position="0 2 1"
     look-controls="enabled: true"
     cursor="fuse: false; rayOrigin: mouse;"
     raycaster="near: 0; far: 10"
     >
      <a-entity cursor="fuse: true; fuseTimeout: 500"
        position="0 0 -1"
        geometry="primitive: ring; radiusInner: 0.005; radiusOuter: 0.01"
        material="color: red">
      </a-entity>
    </a-camera>
    <a-box onclick="alert('box 1')" position="-1 0.5 -3" rotation="0 45 0" color="#4CC3D9" scale="1 0.5 2" material="src: netpower.png" animation="property: position; easing: easeInOutQuad; dir: alternate; dur: 1000; to: -1 1 -3.5; loop: true"></a-box>
    <a-entity onclick="alert('box 2')" position="-2 2 -3" rotation="0 -30 0" geometry="primitive: box; width: 0.5; height: 1; depth: 1.5" material="color: #8855aa; opacity: 0.4; src: #netpower"></a-entity>
    <a-sphere cursor-listener position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
    <a-cylinder event-set__mouseenter="opacity: 0.8" event-set__mouseleave="opacity: 1" position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
    <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>
    <a-entity position="-1 4 -3" light="type: point; intensity: 0.5" animation="property: position; easing: easeInOutQuad; dir: alternate; dur: 1000; to: -1 1 -3.5; loop: true"></a-entity>
    <a-entity id="light" light="type: ambient; color: #ccc"></a-entity>
    <a-sky color="#ECECEC"></a-sky>
  </a-scene>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  mounted(){
    setTimeout(() => {
      var camera = document.querySelector("a-camera");
      camera.components["look-controls"].pitchObject.rotation.x = -0.3;
      camera.components["look-controls"].yawObject.rotation.y = 0.3
    }, 100);

    this.registerCursor()
  },
  methods: {
    registerCursor() {
      window.AFRAME.registerComponent("cursor-listener", {
        init: function () {
          var COLORS = ['blue', 'green', 'red', 'yellow'];
          this.el.addEventListener("click", function (evt) {
            var color = COLORS.shift();
            this.setAttribute("material", "color", color);
            COLORS.push(color);
            console.log("I was clicked at: ", evt.detail.intersection.point);
          });
        },
      });
    },
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
