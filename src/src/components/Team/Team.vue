<template>
  <div >

    <PersoSelector :team="team" @update:selectPlayer="playerSelect">
      <h1 slot-scope="{ player }">From Team : {{ player }}</h1>
    </PersoSelector>
    <Perso :currentPlayer="currentPlayer"></Perso>
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