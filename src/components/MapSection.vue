<template>
  <div class="map" style="height: 60vh; width: 100%">
    <l-map
      v-model="state.zoom"
      v-model:zoom="state.zoom"
      :center="state.center"
    >
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
      ></l-tile-layer>
      <!-- <l-control-layers /> -->
      <l-marker :lat-lng="state.marker">
        <l-icon :icon-url="iconUrl" :icon-size="iconSize" />
      </l-marker>
    </l-map>
  </div>

</template>
<script>
import { LMap, LTileLayer, LMarker, LIcon } from "@vue-leaflet/vue-leaflet";
import "leaflet/dist/leaflet.css";
import { reactive } from "vue";
export default {
  props: ["data"],
  components: {
    LMap,
    LIcon,
    LTileLayer,
    LMarker,
  },
  setup(props) {
    const state = reactive({
      zoom: 6,
      iconWidth: 25,
      iconHeight: 40,
      marker:
        props.data != null
          ? [props.data.location.lat, props.data.location.lng]
          : [0, 0],
      center:
        props.data != null
          ? [props.data.location.lat, props.data.location.lng]
          : [0, 0],
    });
    return { state };
  },
  watch: {
    data() {
      this.state.marker = [this.data.location.lat, this.data.location.lng];
         this.state.center = [this.data.location.lat, this.data.location.lng];
         this.state.zoom = 18
    },
  },
  computed: {
    iconUrl() {
      return require("@/assets/images/location.svg");
    },
    iconSize() {
      return [this.state.iconWidth, this.state.iconHeight];
    },
  },
  methods: {
    changeIcon() {
      this.state.iconWidth += 2;
      if (this.state.iconWidth > this.state.iconHeight) {
        this.state.iconWidth = Math.floor(this.state.iconHeight / 2);
      }
    },
  },
};
</script>
