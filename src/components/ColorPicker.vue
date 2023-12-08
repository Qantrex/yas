<!-- ColorPicker.vue -->

<template>
  <div>
    <div class="color-dot" @click="openColorPicker"></div>
    <div v-if="showColorPicker" class="color-picker">
      <input type="color" v-model="selectedColor" @input="updateColor" />
      <button @click="closeColorPicker">Close</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showColorPicker: false,
      selectedColor: "",
    };
  },
  mounted() {
    // Retrieve the color from localStorage on component mount
    this.selectedColor = localStorage.getItem("accentColor") || "";
  },
  methods: {
    openColorPicker() {
      this.showColorPicker = true;
    },
    updateColor() {
      // Save the selected color to localStorage
      localStorage.setItem("accentColor", this.selectedColor);
      // Emit the color change event
      this.$emit("colorChanged", this.selectedColor);
    },
    closeColorPicker() {
      this.showColorPicker = false;
    },
  },
};
</script>

<style scoped>
.color-dot {
  width: 20px;
  height: 20px;
  background-color: var(--accent-color);
  border-radius: 50%;
  cursor: pointer;
  position: fixed;
  bottom: 20px;
  right: 20px;
}

.color-picker {
  position: absolute;
  bottom: 0;
  right: 0;
  padding: 10px;
  background-color: #fff;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}
</style>