<template>
  <div class="header">
    <h1 class="header__heading">IP Address Tracker</h1>
    <input-with-validation @getData="getData"></input-with-validation>
  </div>
</template>
<script>
import InputWithValidation from "./InputWithValidation.vue";
export default {
  components: { InputWithValidation },
  emits:["getData"],
    setup(props,context) {
    const getData = (ipAddress) =>{
      context.emit("getData", ipAddress)

    }
    return{getData}
  }
};
</script>
