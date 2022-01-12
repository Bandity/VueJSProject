<template >
  <div>
    <div style="display: flex">
      <div style="flex: 7 7">
        <Team
          :currentShop="currentShop"
          :currentPlayer="currentPlayer"
          :team="team"
          @change:selectPlayer="playerSelect"
        />
      </div>
      <div style="flex: 8 8">
        <World
          :currentTown="currentTown"
          :currentStreet="currentStreet"
          :currentShop="currentShop"
          :towns="towns"
          @change:selectedTown="selectedTown"
          @change:selectedShop="selectedShop"
          @change:selectedStreet="selectedStreet"
          @change:shop="shopUsed"
        />
      </div>
    </div>
  </div>
</template>

<script>
import Team from "./components/Team/Team.vue";
import World from "./components/World/World.vue";
import { towns, team } from "./model/model";

export default {
  name: "App",
  components: {
    Team,
    World,
  },
  data: () => {
    return {
      currentShop: null,
      currentTown: null,
      currentPlayer: null,
      currentStreet: null,
      towns,
      team,
    };
  },
  methods: {
    shopUsed(event) {
      this.currentShop = event;
    },

    selectedTown(id) {
      this.currentTown = towns[id];
    },
    selectedStreet(id) {
      this.currentStreet = this.currentTown.streets[id];

    },
    selectedShop(id) {
      this.currentShop = this.currentStreet.shops[id];
    },

    playerSelect(id) {
      this.currentPlayer = this.team[id];
    },
  },
};
</script>
<style>
</style>
