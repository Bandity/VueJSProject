<template>
  <div v-if="streetName !== null">
    <select @change="eventShopSelectorEmmiter($event)">
      <option value="null" disabled selected="selected">Please Select a Shop</option>
      <option v-for="(el, i) in shops " :key="i" :value="i">
        {{ el }}
      </option>
    </select>
  </div>
</template>

<script>
export default {
  name: "ShopSelector",
  props: {
    shops: Array,
    streetName: String
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    eventShopSelectorEmmiter(event) {
      this.$emit("update:selectedShop",event);
    }
  },
};
</script>

<style>
</style>