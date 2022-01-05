<template>
  <div>
    <TownSelector/>
    <StreetSelector/>
    <Shop/>
    <ShopSelector/>
  </div>
</template>

<script>
import TownSelector from "./Town/TownSelector.vue";
import StreetSelector from "./Street/StreetSelector.vue";
import Shop from "./Shop/Shop.vue"
import ShopSelector from "./Shop/ShopSelector.vue";
export default {
  name: "World",
  components: {
    TownSelector,
    StreetSelector,
    Shop,
    ShopSelector
  }

}
</script>

<style>

</style>