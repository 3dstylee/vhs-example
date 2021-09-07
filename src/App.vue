<template>
  <v-app>
    <div id="front" class="mt-2 mx-2">
      <v-btn fab color="primary" @click="add"><v-icon>mdi-plus</v-icon></v-btn>
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
          opacity="0.3"
        />
        <template v-for="(item, index) in items">
          <a-entity
            :id="index"
            :key="index"
            class="item"
            gltf-model="/sofa.glb"
            :position="item.position"
          />
        </template>
        <a-entity
          v-if="isMoving"
          allocate
          cursor="rayOrigin: mouse"
          raycaster="objects: #plane"
          @collide="move"
          @mouseup="place"
        />
        <a-entity
          v-else
          cursor="rayOrigin: mouse"
          raycaster="objects: .item"
          @mouseup="select"
        />
      </a-scene>
    </div>
  </v-app>
</template>

<script>
import aframe from "aframe";

aframe.registerComponent("allocate", {
  dependencies: ["raycaster"],

  tick() {
    const intersections = this.el.components.raycaster.intersections;
    if (intersections.length) {
      this.el.emit("collide", intersections);
    }
  },
});

export default {
  data() {
    return {
      items: [],
      selectedItemIndex: -1,
      isMoving: false,
    };
  },

  methods: {
    add() {
      this.isMoving = true;
      this.items.push({ position: { x: 0, y: 0, z: 0 } });
      this.selectedItemIndex = this.items.length - 1;
    },

    select(e) {
      const intersection = e.detail.intersectedEl;
      if (!intersection) return;

      this.selectedItemIndex = intersection.id;
      this.isMoving = true;
    },

    move(e) {
      const position = e.detail[0].point;
      this.$set(this.items[this.selectedItemIndex], "position", position);
    },

    place() {
      this.isMoving = false;
      this.selectedItemIndex = -1;
    },
  },
};
</script>

<style>
#front {
  z-index: 1000;
}
</style>
