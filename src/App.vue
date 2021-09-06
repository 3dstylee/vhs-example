<template>
  <div>
    <a-scene>
      <a-assets>
        <img id="sky_img" src="./assets/room.jpg" alt="No image" />
      </a-assets>
      <a-sky id="sky" src="#sky_img" />
    </a-scene>
  </div>
</template>

<script>
import "aframe";

export default {};
</script>
