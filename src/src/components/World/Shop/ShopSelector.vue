<template>
  <div v-if="streetName !== null">
    <div
      v-for="(el, i) in shops"
      :key="i"
      
    >
      <input
        type="radio"
        :value="i"
        name="shops"
        @change="eventShopSelectorEmmiter($event)"
      />
      <label>{{ el }}</label
      ><br />
    </div>
  </div>
</template>

<script>
export default {
  name: "ShopSelector",
  props: {
    shops: Array,
    streetName: String,
  },
  data: () => {
    return {};
  },
  computed: {},
  methods: {
    eventShopSelectorEmmiter(event) {
      let id = event.target.value;
      this.$emit("change:selectedShop", id);
    },
  },
};
</script>

<style>
</style>