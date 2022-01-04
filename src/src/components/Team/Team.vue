<template>
  <div>
    <PersoSelector :team="team" :currentPlayer="this.currentPlayer" />
    <Perso />
    {{this.currentPlayer}}
  </div>
</template>

<script>
import PersoSelector from "./PersoSelector.vue";
import Perso from "./Perso.vue";
import { towns, team } from "../../model/model";
export default {
  name: "Team",
  components: {
    PersoSelector,
    Perso,
  },
  data: () => {
    return {
      currentTowns: towns,
      team,
      currentPlayer:"",
    };
  },
  computed: {},
  methods: {
    selectPlayer(event) {
      let id = event.target.value;
      this.currentPlayer = this.$props.team[id].name
    }
  }
};
</script>

<style>
</style>