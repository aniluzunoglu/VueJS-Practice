<template>
  <div id="app">
    <search v-on:searchRequested="handleSearch"></search>
    <p v-if="isLoading">Loading</p>
    <preview v-bind:gifs="gifs"></preview>
  </div>
</template>

<script>
import preview from "./components/preview.vue";
import search from "./components/search.vue";
export default {
  name: "app",
  components: { search, preview },
  data() {
    return {
      gifs: [],
      isLoading: true,
    };
  },
  methods: {
    handleSearch(query) {
      this.gifs = [];
      this.isLoading = true;
      fetch(
        `https://api.giphy.com/v1/gifs/search?api_key=Koc5Zh8obOmjL4Oj88g2kV8da46wI3P6&q=${query}&limit=25&offset=0&rating=g&lang=en`
      )
        .then((res) => {
          return res.json();
        })
        .then((res) => {
          this.gifs = res.data;
          this.isLoading = false;
        });
    },
  },
  created() {
    fetch(
      "https://api.giphy.com/v1/gifs/trending?api_key=Koc5Zh8obOmjL4Oj88g2kV8da46wI3P6&limit=25&rating=g"
    )
      .then((res) => {
        return res.json();
      })
      .then((res) => {
        this.gifs = res.data;
        this.isLoading = false;
      });
  },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>


