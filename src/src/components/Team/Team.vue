<template>
  <div>
      <PersoSelector/>
      <Perso/>
  </div>
</template>

<script>
import PersoSelector from "../model./components/PersoSelector.vue";
import Perso from "../model./components/Perso.vue";
export default {
    name: "Team",
    components: {
        PersoSelector,
        Perso
    }
}
</script>

<style>

</style>