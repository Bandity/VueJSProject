<template >
  <div>
    <link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Lato:wght@300&family=Poppins:wght@400;700&family=Roboto:wght@400;700&display=swap" rel="stylesheet">
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
      this.currentShop =null;
      this.currentStreet = null;
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
body{ 
  color: white;
  font-family: 'Poppins', sans-serif;
background:rgba(15,15,15,1);
}
input {
  border: 2px solid red;
  border-radius: 4px;
}
input[readonly] {
  width: 500px;
}

button{
    background-color: #4CAF50; /* Green */
  border: none;
  color: white;
  padding: 1px 22px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  border-radius: 4px;
}

table {
  border-collapse: collapse;
}
tr{
  padding: 10px 10px 10px 10px;
}
td{
  padding: 10px 10px 10px 10px;
}
</style>
