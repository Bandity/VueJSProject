<template>
  <div >
    <PersoSelector :team="team" @update:selectPlayer="playerSelect"/>
    <Perso :currentPlayer="currentPlayer" :currentShop="currentShop"/>
  </div>
</template>

<script>
import PersoSelector from "./PersoSelector.vue";
import Perso from "./Perso.vue";
import { team } from "../../model/model";
export default {
  name: "Team",
  components: {
    PersoSelector,
    Perso,
  },
  props: {
    currentShop : Object,
  },
  data: () => {
    return {
      team: team,
      currentPlayer: null,
    };
  },
  computed: {},
  methods: {
    playerSelect(value) {
      let id = value.target.value;
      this.currentPlayer = this.team[id];
    },
  },
};
</script>

<style>
  
</style>