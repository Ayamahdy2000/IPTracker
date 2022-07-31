<template>
  <div class="form-group">
    <input
      type="text"
      v-model="state.IPAdress"
      @blur="v.IPAdress.$touch"
      class="form-group__input"
      placeholder="Search for any IP address or domain"
    />
    <div class="form-group__icon" @click="getData">
      <span class="icon-keyboard_arrow_down form-group__icon__arrow"></span>
    </div>
    <div
      class="form-group__error"
      v-for="(error, errorIndex) in v.IPAdress.$errors"
      :key="errorIndex"
    >
      {{ error.$message }}
    </div>
  </div>
</template>
<script>
import useVuelidate from "@vuelidate/core";
import { required, helpers } from "@vuelidate/validators";
import { reactive, computed } from "vue";
const onlyDigits = (value) => {
  if (typeof value === "undefined" || value === null || value === "") {
    return true;
  }
  return /^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/.test(
    value
  );
};
export default {
  setup() {
    const state = reactive({
      IPAdress: null,
    });

    const rules = computed(() => {
      return {
        IPAdress: {
          required: helpers.withMessage("IP Address Required", required),
          onlyDigits: helpers.withMessage(
            "Valid IP Address Required",
            onlyDigits
          ),
        },
      };
    });
    const v = useVuelidate(rules, state);

    return { state, v };
  },
  methods: {
    getData() {
      this.v.$validate();
      if (!this.v.$error) {
        this.$emit("getData", this.state.IPAdress);
      }
    },
  },
};
</script>
