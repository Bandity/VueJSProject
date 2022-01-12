<template>
  <div >
    <PersoSelector :team="team" @change:selectPlayer="eventPlayerEmmiter"/>
    <Perso :currentPlayer="currentPlayer" :currentShop="currentShop" />
  </div>
</template>

<script>
import PersoSelector from "./PersoSelector.vue";
import Perso from "./Perso.vue";

export default {
  name: "Team",
  components: {
    PersoSelector,
    Perso,
  },
  props: {
    currentPlayer: Object,
    currentShop : Object,
    team: Array
  },
  data: () => {
    return {
    };
  },
  computed: {
  },
  methods: {
    eventPlayerEmmiter(playerSelected) {
      this.$emit("change:selectPlayer",playerSelected);
    }
  },
};
</script>

<style>
  
</style>