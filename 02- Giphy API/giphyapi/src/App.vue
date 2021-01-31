<template>
  <div id="app">
    <search></search>
    <preview v-bind:gifs="gifs"></preview> 
  </div>
</template>

<script>
import Preview from "./components/preview.vue";
import search from "./components/search.vue";
export default {
  name: "app",
  components: { search, Preview },
  data() {
    gifs: [];
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
        console.log(res.data);
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
