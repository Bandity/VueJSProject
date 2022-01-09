<template>
  <div>
    <div style="display: flex">
      <div style="flex: 7 7">
    <Team :currentShop="currentShop"/>
      </div>
    <div style="flex: 8 8">
    <World  @update:shop="shopUsed"/>
    </div>
    </div>
  </div>
</template>

<script>
import Team from "./components/Team/Team.vue";
import World from "./components/World/World.vue";

export default {
  name: "App",
  components: {
    Team,
    World,
  },
  data: () => {
    return {
      currentShop: null,
      currentTown : null,
      currentPerso: null,
      currentStreet: null,
    }
  },
  methods: {
    shopUsed(event){
      this.currentShop = event;
    }
  }
};
</script>
<style>

</style>
