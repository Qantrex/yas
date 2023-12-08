<template>
  <div id="app">
    <!-- Allows users to pick accent color -->
    <ColorPicker @colorChanged="updateAccentColor" />
    <!-- Basic Search Bar with 3 Search Engines -->
    <SearchBar />
    <!-- Displays Quick Links in different Categories -->
    <QuickLinks />
    <CustomCursor />
  </div>
</template>

<script>
import SearchBar from "@/components/SearchBar.vue";
import QuickLinks from "@/components/QuickLinks.vue";
import ColorPicker from "@/components/ColorPicker.vue";
import CustomCursor from '@/components/CustomCursor.vue';

export default {
  name: "App",
  components: {
    SearchBar,
    QuickLinks,
    ColorPicker,
    CustomCursor,
  },
  methods: {
    // Method to update the accent color based on ColorPicker selection
    updateAccentColor(newColor) {
      document.documentElement.style.setProperty("--accent-color", newColor);
    },
  },
};
</script>

<style>
/* Importing the Open Sans font from Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Open+Sans&display=swap');

/* Removes the default cursor */
* {
  cursor: none;
}

html, body {margin: 0; height: 100%; overflow: hidden}

#app {
  font-family: 'Open Sans', sans-serif;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  color: var(--accent-color);
}

body {
  background-color: #000;
  color: #fff;
}

/* Light Blue Accent Color */
:root {
  --accent-color: #00bcd4;
  --cursor-color: #ffffff;
}
</style>