<template>
  <v-app>
    <div id="front" class="mt-2 mx-2">
      <v-btn fab color="primary"><v-icon>mdi-plus</v-icon></v-btn>
    </div>
    <div style="height: 0">
      <a-scene vr-mode-ui="enabled: false">
        <a-assets>
          <img id="sky_img" src="./assets/room.jpg" alt="No image" />
        </a-assets>
        <a-sky id="sky" src="#sky_img" />
        <a-plane
          id="plane"
          height="20"
          width="20"
          rotation="-90 0 0"
          position="0 -1.3 0"
          opacity="0.3"
        />
        <a-entity gltf-model="/sofa.glb" />
      </a-scene>
    </div>
  </v-app>
</template>

<script>
import "aframe";

export default {};
</script>

<style>
#front {
  z-index: 1000;
}
</style>
