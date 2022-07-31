<template>
  <div class="tracker">
    <header-section @getData="getData"></header-section>
    <location-data :loading="state.loading" :data="state.data"></location-data>
    <map-section :data="state.data"></map-section>
  </div>
</template>

<script>
import HeaderSection from "./components/HeaderSection.vue";
import LocationData from "./components/LocationData.vue";
import MapSection from "./components/MapSection.vue";
import axios from "axios";
import { reactive } from "vue";
export default {
  name: "App",
  components: { HeaderSection, LocationData, MapSection },
  setup() {
    const state = reactive({
    
      data: null,
      loading: false,
    });
    const getData = (ipAddress) => {
      state.loading = true;
      axios
        .get(
          `https://geo.ipify.org/api/v2/country,city?apiKey=at_txjvfLQeGNvNJ6VzBdO5UjJBdowCy&ipAddress=${ipAddress}`
        )
        .then((res) => {
          state.data = res.data;
        })
        .finally(() => (state.loading = false));
    };
    return { state, getData };
  },
};
</script>

<!-- Main style -->
<style lang="scss">
@import "assets/styles/main.scss";
</style>
