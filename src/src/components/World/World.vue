<template>
  <div id="World-Container">
    <TownSelector :townNames="[towns[0].name, towns[1].name, towns[2].name]" @update:selectedTown="selectedTown" />
    <StreetSelector  />
    <Shop />
    <ShopSelector />
  </div>
</template>

<script>
import TownSelector from "./Town/TownSelector.vue";
import StreetSelector from "./Street/StreetSelector.vue";
import Shop from "./Shop/Shop.vue";
import ShopSelector from "./Shop/ShopSelector.vue";
import {towns} from "../../model/model";
export default {
  name: "World",
  components: {
    TownSelector,
    StreetSelector,
    Shop,
    ShopSelector,
  },
  data: () => {
    return {
      currentTown: null,
      currentStreet: null,
      currentShop: null,
      towns
    };
  },
  methods: {
    selectedTown(event) {
      let id = event.target.value;
      this.currentTown = towns[id];
    }
  }
};
</script>

<style>
#World-Container {
  display: flex;
  flex-direction: column;
  flex: 7;
}
</style>