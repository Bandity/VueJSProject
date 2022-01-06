<template>
  <div v-if="townName !== null" style="width: 50%">
        <div style="display: flex">
      <div style="width: 50%">
        <div v-for="(el, i) in streets" :key="i">
          <input
            type="radio"
            :value="i"
            name="streets"
            @click="eventStreetSelectorEmmiter($event)"
          />
          <label>{{ el }}</label
          ><br />
        </div>
        <!-- EXO 2.1 : liste à puce des rues pour sélectionner la rue courante -->
      </div>
  </div>
  </div>
</template>

<script>
export default {
  name: "StreetSelector",
  props: {
    streets: Array,
    townName : String
  },
  data: () => {
    return {
    };
  },
  computed: {},
  mounted:()=> {
  },
  methods: {
    eventStreetSelectorEmmiter(event) {
      this.$emit("update:selectedShop",event);
    }
  },
};
</script>

<style>
</style>