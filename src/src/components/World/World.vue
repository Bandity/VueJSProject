<template>
  <div>
    <br />
    <TownSelector
      :townsNames="townsNames"
      @change:selectedTown="eventTownEmmiter"
    />
    <h3 v-if="this.townName !== null" style="text-align: center">
      {{ this.townName }}
    </h3>
    <br />
    <StreetSelector
      :streets="streets"
      :townName="townName"
      :numberShops="shopsInfo"
      :catShops="shopsNumberOfItems"
      @change:selectedStreet="eventStreetSelectorEmmiter"
    />
    <h3 v-if="this.currentStreet !== null" style="text-align: center">
      {{ this.currentStreet.name }}
    </h3>
    <br />
    <ShopSelector
      :shops="shop"
      :streetName="streetName"
      :shopsCats="shopCategory"
      @change:selectedShop="eventShopSelectorEmmiter"
    />
    <br />
    <Shop :currentShop="currentShop">
      <h3
        slot-scope="{ shopName }"
        style="display: flex; align-items: center; justify-content: center"
      >
        {{ shopName }}
      </h3>
    </Shop>
    <br />
  </div>
</template>

<script>
import TownSelector from "./Town/TownSelector.vue";
import StreetSelector from "./Street/StreetSelector.vue";
import Shop from "./Shop/Shop.vue";
import ShopSelector from "./Shop/ShopSelector.vue";

export default {
  name: "World",
  components: {
    TownSelector,
    StreetSelector,
    Shop,
    ShopSelector,
  },
  props: {
    currentShop: Object,
    currentTown: Object,
    currentStreet: Object,
    towns: Array,
  },
  data: () => {
    return {
      townsNames: [],
      shopName: null,
      items: [],
      itemsOrder: [],
    };
  },
  created() {
    this.init();
  },
  computed: {
    streets() {
      let street = [];
      if (this.currentTown !== null) {
        for (let i = 0; i < this.currentTown.streets.length; i++) {
          street.push(this.currentTown.streets[i].name);
        }
      }
      return street;
    },
    shop() {
      let shops = [];
      if (this.currentStreet !== null) {
        for (let i = 0; i < this.currentStreet.shops.length; i++) {
          shops.push(this.currentStreet.shops[i].name);
        }
      }
      return shops;
    },
    shopsInfo() {
      let info = [];
      if (this.currentTown !== null){
        for (let i = 0; i < this.currentTown.streets.length; i++) {
          info.push(this.currentTown.streets[i].shops.length);
        }
          
      }
      return info;
    },
    shopsNumberOfItems() {
      let numberOfItems = [];
      if (this.currentTown !== null){
        for (let i = 0; i < this.currentTown.streets.length; i++) {
          let count =0;
          for (let j = 0; j < this.currentTown.streets[i].shops.length; j++){
            count += this.currentTown.streets[i].shops[j].itemStock.length
          }
          numberOfItems.push(count);
        }
      }
      return numberOfItems;
    },
    shopCategory() {
      let category = [];
      if(this.currentStreet !== null){
        for (let i = 0; i < this.currentStreet.shops.length; i++){
          //console.log(this.currentStreet.shops[i].itemCat);
          category.push(this.currentStreet.shops[i].itemCat)

        }
      }
      return category;
    },
    shopSelected() {
      let shopName = "";
      if (this.currentShop !== null || this.currentShop !== undefined) {
        shopName = this.currentShop.name;
        this.$emit("change:shop", this.currentShop);
      }
      return shopName;
    },
    townName() {
      if (this.currentTown !== null) {
        return this.currentTown.name;
      }
      return null;
    },
    streetName() {
      if (this.currentStreet !== null) {
        return this.currentStreet.name;
      }
      return null;
    },
  },
  methods: {
    init() {
      for (let i = 0; i < this.towns.length; i++) {
        this.townsNames.push( this.towns[i].name);
      }
    },
    eventTownEmmiter(townSelected) {
      this.$emit("change:selectedTown", townSelected);
    },
    eventShopSelectorEmmiter(shopSelected) {
      this.$emit("change:selectedShop", shopSelected);
    },
    eventStreetSelectorEmmiter(streetSelected) {
      this.$emit("change:selectedStreet", streetSelected);
    },
  },
};
</script>

<style>
</style>