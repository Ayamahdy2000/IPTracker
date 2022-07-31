<template>
  <div class="location">
    <div class="text-center" v-if="loading">
      <div class="spinner-border" role="status"></div>
    </div>

    <div class="location__grid" v-if="data != null && !loading">
      <div class="location__card" v-if="data && data.ip">
        <p class="location__card__head">ip address</p>
        <p class="location__card__value">{{ data.ip }}</p>
      </div>
      <div class="location__card" v-if="data && data.location">
        <p class="location__card__head">Location</p>
        <p class="location__card__value">
          {{ data.location.country }} ,{{ data.location.city }}
        </p>
      </div>
      <div class="location__card" v-if="data && data.location">
        <p class="location__card__head">Timezone</p>
        <p class="location__card__value">{{ data.location.timezone }}</p>
      </div>
      <div class="location__card" v-if="data && data.isp">
        <p class="location__card__head">isp</p>
        <p class="location__card__value">{{ data.isp }}</p>
      </div>
    </div>
    <p class="location__no-data" v-if="data==null && !loading">Search for any IP address or domain</p>
  </div>
</template>
<script>
export default {
  props: ["loading", "data"],
};
</script>
