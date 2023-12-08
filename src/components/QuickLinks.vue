<!-- QuickLinks.vue -->

<template>
  <div class="quick-links">
    <!-- Loop through categories -->
    <div v-for="category in categories" :key="category.id" class="category">
      <!-- Category name -->
      <h3>{{ category.name }}</h3>
      <!-- Loop through links within the category -->
      <a v-for="link in category.links" :key="link.id" :href="link.url" class="quick-link">
        {{ link.text }}
      </a>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    // Data properties for quick link categories and their respective links
    return {
      categories: [
        {
          id: 1,
          name: '<School/>',
          links: [
            { id: 1, text: 'Mail', url: 'https://owa.tgm.ac.at' },
            { id: 2, text: 'E-Learning', url: 'https://elearning.tgm.ac.at' },
            { id: 3, text: 'Webuntis', url: 'https://neilo.webuntis.com/' },
            { id: 4, text: 'Digi4School', url: 'https://digi4school.at/ebooks' }
          ]
        },
        {
          id: 2,
          name: '<Coding/>',
          links: [
            { id: 4, text: 'GPT', url: 'https://chat.openai.com' },
            { id: 3, text: 'Roadmap.sh', url: 'https://roadmap.sh/' },
            { id: 4, text: 'Leetcode', url: 'https://leetcode.com/' },
            { id: 4, text: 'StackOverflow', url: 'https://stackoverflow.com/' }
          ]
        },
        {
          id: 3,
          name: '<Essentials/>',
          links: [
            { id: 5, text: 'GitHub', url: 'https://github.com/' },
            { id: 5, text: 'Youtube', url: 'https://www.youtube.com' },
            { id: 5, text: 'Willhaben', url: 'https://www.willhaben.at/iad' },
            { id: 5, text: 'Amazon', url: 'https://www.amazon.de/' }
          ]
        }
      ]
    };
  },
};
</script>

<style scoped>
.quick-links {
  display: flex;
  flex-direction: row;
  align-items: flex-start;
}

.category {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-right: 45px;
}

.quick-link {
  color: #fff;
  text-decoration: none;
  padding: 10px;
  transition: color 0.3s ease, text-shadow 0.3s ease; /* Add text-shadow to the transition */
}

.quick-link:hover {
  color: #fff; /* Change the color on hover to white */
  text-shadow:
    0 0 7px white,
    0 0 10px white,
    0 0 21px white,
    0 0 42px white,
    0 0 82px white;
  background-color: black;
  animation: ease-in-out infinite alternate;
}
</style>