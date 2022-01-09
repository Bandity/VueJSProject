<template>
  <div>
    <PersoCaracs :currentPlayer="currentPlayer"/>
    <PersoSlots :currentPlayer="currentPlayer"/>
    <PersoOps :currentPlayer="currentPlayer" :currentShop="currentShop"/>
  </div>
</template>

<script>
import PersoCaracs from "./Player/PersoCaracs.vue";
import PersoOps from "./Player/PersoOps.vue";
import PersoSlots from "./Player/PersoSlots.vue";

export default {

  name: "Perso",
  components:{
    PersoCaracs,
    PersoOps,
    PersoSlots
  },
  props: {
    currentPlayer: Object,
    currentShop: Object
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    
  },
}
</script>

<style>

</style>