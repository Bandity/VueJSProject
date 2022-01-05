<template>
  <div id="World-Container">
    <TownSelector :townNames="[towns[0].name, towns[1].name, towns[2].name]" @update:selectedTown="selectedTown" />
    <StreetSelector  :streets="streets" :townName="townName" @update:selectedStreet="selectedStreet" />
    <Shop />
    <ShopSelector :shops="shops" :streetName="streetName" @update:selectedShop="selectedShop" />
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
      townName : null,
      streetName : null,
      towns,
      streets:[],
      shops:[]
    };
  },
  methods: {
    selectedTown(event) {
      let id = event.target.value;
      this.currentTown = towns[id];
      this.townName = this.currentTown.name;
      for(let i = 0; i < this.currentTown.streets.length; i++){
        this.streets[i] = this.currentTown.streets[i].name;
      }
    },
    selectedStreet(event){
      let id = event.target.value;
      this.currentStreet = this.streets[id];
      for(let i = 0; i < this.currentStreet.shops.length; i++){
        this.shops[i] = this.currentStreet.shops[i].name;
      }
    },
    selectedShop(event){
      let id = event.target.value;
      this.currentShop = this.shops[id];
      
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