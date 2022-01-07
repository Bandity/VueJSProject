<template>
  <div v-if="currentShop !== null && shopName !==null">
    <slot :shopName="currentShop.name"></slot>
    <div id="list_store" v-if="currentShop != null">
      <div style="width: 50%">
        <h4>In stock</h4>
        <ol>
          <li v-for="(item, i) in currentShop.itemStock" :key="i">
            {{ item.name }}
            {{ item.price }} $
          </li>
        </ol>
      </div>
      <div>
        <h4>To order</h4>
        <ol>
          <li v-for="(item, i) in currentShop.itemOrder" :key="i">
            {{ item.name }}
            {{ item.price }} $
          </li>
        </ol>
      </div>
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
      shopName: "",
    };
  },
  methods: {
    eventPlayerEmmiter(event) {
      this.$emit("update:selectPlayer", event);
    },
  },
};
</script>

<style scoped>
#list_store {
  display: flex; 
  align-items: center; 
  justify-content: center;
  background: #a29f9f;
  border: 1px solid;
  border-radius: 60px;
  padding: 40px;
}
</style>