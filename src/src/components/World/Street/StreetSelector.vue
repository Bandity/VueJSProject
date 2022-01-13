<template>
  <div v-if="townName !== null" style="width: 50%">
        <div style="display: flex">
      <div style="width: 50%">
        <div v-for="(el, i) in streets" :key="i">
          <input type="checkbox" :value="i" name="streets" @click="eventStreetSelectorEmmiter($event) "> 
          <label>{{ el }}</label
          ><br />
        </div>
      </div>
      <div v-if="numberShops.length > 0" >
        <div v-for="(el, i) in numberShops" :key="i"><label v-if="el !== 1">{{el}} Shops</label><label v-if="el=== 1">{{el}} Shop</label></div>
      </div>
      <div v-if="catShops.length > 0" >
        <div v-for="(el, i) in catShops" :key="i"><label style="padding-left: 10px" v-if="el !== 1">{{el}} Items</label></div>  
      </div>
  </div>
  </div>
</template>

<script>
export default {
  name: "StreetSelector",
  props: {
    streets: Array,
    townName : String,
    numberShops: Array,
    catShops: Array,
  },
  data: () => {
    return {
    };
  },
  computed: {},
  mounted:()=> {
  },
  methods: {
    eventStreetSelectorEmmiter(event) {    
      let id = event.target.value;
      this.$emit("change:selectedStreet",id); 
    },
  },
};
</script>

<style>
</style>