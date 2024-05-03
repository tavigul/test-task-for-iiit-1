<template>
  <div class="app">
    <MainPage />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import MainPage from "./views/MainPage.vue";

export default defineComponent({
  name: "App",
  components: {
    MainPage,
  },
});
</script>

<style>
body {
  background: hsl(233, 40%, 8%);
}
</style>
