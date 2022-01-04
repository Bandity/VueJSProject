<template>
  <div>
    <Team />
    <World />
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
