<template>
  <div id="World-Container">
    <TownSelector :townsNames="townsNames" @update:selectedTown="selectedTown" />
    <StreetSelector  :streets="streets" :townName="townName" @update:selectedShop="selectedStreet" />
    <ShopSelector :shops="shops" :streetName="streetName" @update:selectedShop="selectedShop" />
    <Shop :currentShop="currentShop">
      <h1 slot-scope="{ shopName }">{{ shopName }}</h1>
    </Shop>
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
      townsNames: [],
      townName: null,
      streetName : null,
      shopName : null,
      towns,
      items:[],
      itemsOrder:[],
      streets:[],
      shops:[]
    };
  },
  created() {
    this.init()
  },
  methods: {
    init() {
      for(let i = 0; i <towns.length; i++){
        this.townsNames[i] = this.towns[i].name
      }
    },
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
      this.currentStreet = this.currentTown.streets[id];
      this.streetName = this.currentStreet.name
      for(let i = 0; i < this.currentStreet.shops.length; i++){
        this.shops[i] = this.currentStreet.shops[i].name;
      }
    },
    selectedShop(event){
      let id = event.target.value;
      console.log(id)
      this.currentShop = this.currentStreet.shops[id];
      this.shopName = this.currentShop.name;
    },
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