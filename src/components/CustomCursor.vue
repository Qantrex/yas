<!-- CustomCursor.vue -->

<template>
  <!-- Custom cursor element with dynamic positioning -->
  <div class="custom-cursor" :style="{ left: `${cursorX}px`, top: `${cursorY}px` }"></div>
</template>

<script>
export default {
  data() {
    // Current Cursor Position
    return {
      cursorX: 0,
      cursorY: 0,
    };
  },
  methods: {
    // Method to update cursor position based on mousemove event
    updateCursorPosition(event) {
      this.cursorX = event.clientX;
      this.cursorY = event.clientY;
    },
  },
  mounted() {
    // Listen for mousemove events to update cursor position
    window.addEventListener('mousemove', (event) => {
      this.updateCursorPosition(event);
    });
  },
};
</script>

<style scoped>
.custom-cursor {
  position: fixed;
  width: 15px;
  height: 15px;
  background-color: var(--cursor-color);
  border-radius: 50%;
  pointer-events: none;
  z-index: 9999;
  transform: translate(-50%, -50%);
}
</style>