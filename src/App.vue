<template>
  <div>
    <a-scene>
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
</template>

<script>
import "aframe";

export default {};
</script>
