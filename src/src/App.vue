<template>
  <div>
    <div style="display: flex">
      <div style="flex: 7 7">
    <Team />
      </div>
    <div style="flex: 8 8">
    <World />
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
};
</script>
