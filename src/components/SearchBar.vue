<!-- SearchBar.vue -->

<template>
  <!-- Search bar container -->
  <div class="search-bar">
    <!-- Input for user search query -->
    <input
      v-model="searchQuery"
      @focus="expandSearchBar"
      @blur="collapseSearchBar"
      @keydown.enter.prevent="handleEnterKey"
      placeholder="\_(^-^)_/"
    />
    <!-- Dropdown to select search engine -->
    <select v-model="selectedEngine">
      <option value="ddg">DuckDuckGo</option>
      <option value="bs">Brave Search</option>
      <option value="sxng">SearxNG</option>
    </select>
  </div>
</template>

<script>
export default {
  data() {
    // Data properties for search query, selected search engine, and search bar state
    return {
      searchQuery: "",
      selectedEngine: "ddg",
      isSearchBarExpanded: false,
    };
  },
  methods: {
    // Method to expand the search bar on focus
    expandSearchBar() {
      this.isSearchBarExpanded = true;
    },
    // Method to collapse the search bar on blur
    collapseSearchBar() {
      this.isSearchBarExpanded = false;
    },
    // Method to handle Enter key press for searching
    handleEnterKey() {
      if (this.searchQuery.trim() !== "") {
        const searchUrl = this.getSearchUrl();
        console.log("Search URL:", searchUrl);
        this.searchQuery = "";
        window.open(searchUrl, "_blank");
      } else {
        // Clear search query if empty on Enter key press
        this.searchQuery = "";
      }
    },
    // Method to construct the search URL based on the selected search engine
    getSearchUrl() {
      const query = encodeURIComponent(this.searchQuery);
      const engine = this.selectedEngine;
      const engines = {
        ddg: "https://duckduckgo.com/?q=",
        bs: "https://search.brave.com/search?q=",
        sxng: "https://search.hbubli.cc/search?q=",
      };
      return engines[engine] + query;
    },
  },
};
</script>

<style scoped>
.search-bar {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 20px;
}

.search-bar input {
  color: white;
  background-color: black;
  padding: 10px;
  width: 200px;
  text-align: center;
  border: 2px solid var(--accent-color);
  border-radius: 5px;
  outline: none;
  transition: width 0.3s ease;
}

.search-bar input:focus {
  width: 300px;
}

.search-bar select {
  margin-left: 10px;
  padding: 8px;
  border: 2px solid var(--accent-color);
  border-radius: 5px;
  outline: none;
  background-color: #000;
  color: #fff;
}
</style>