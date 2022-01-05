<template>
  <div style="display: flex" v-if="currentShop != null">
    <slot :shopName="shopName"></slot>
    <div style="width: 50%">
      <h4>In stock</h4>
      <ol>
        <li v-for="(item, i) in currentShop.itemStock" :key="i">
          {{ item.name }}
          {{ item.price }} $
        </li>
      </ol>
    </div>
    <div style="width: 50%">
      <h4>To order</h4>
      <ol>
        <li v-for="(item, i) in currentShop.itemOrder" :key="i">
          {{ item.name }}
          {{ item.price }} $
        </li>
      </ol>
    </div>
  </div>
</template>

<script>
export default {
  name: "Shop",
  props: {
    currentShop: Object,
  },
  data: () => {
    return {
      shopName: ""
    };
  },
  methods: {
    eventPlayerEmmiter(event) {
      this.$emit("update:selectPlayer", event);
    },
  },
};
</script>

<style>
</style>