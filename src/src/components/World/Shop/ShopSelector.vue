<template>
  <div v-if="streetName !== null">
    <div v-for="(el, i) in shops" :key="i">
      <input
        type="radio"
        :value="i"
        name="shops"
        @change="eventShopSelectorEmmiter($event)"
      />
      {{el}}<br />
      
    </div>
  </div>
</template>

<script>
export default {
  name: "ShopSelector",
  props: {
    shops: Array,
    streetName: String,
    shopsCats: Array,
  },
  data: () => {
    return {
      str:null,
    };
  },
  computed: {
    
  },
  methods: {
    eventShopSelectorEmmiter(event) {
      let id = event.target.value;
      this.$emit("change:selectedShop", id);
    },
  },
};
</script>

<style>
h1{
  flex-wrap: wrap;
}
</style>