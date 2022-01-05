<template>
  <div>
    <PersoCaracs :currentPlayer="currentPlayer"/>
    <PersoOps :currentPlayer="currentPlayer"/>
    <PersoSlots :currentPlayer="currentPlayer"/>
  </div>
</template>

<script>
import PersoCaracs from "./Player/PersoCaracs.vue";
import PersoOps from "./Player/PersoOps.vue";
import PersoSlots from "./Player/PersoSlots.vue";

export default {

  name: "Perso",
  components:{
    PersoCaracs,
    PersoOps,
    PersoSlots
  },
  props: {
    currentPlayer: Object,
  },
  data: () => {
    return {
    };
  },
  computed: {},
  methods: {
    selectPlayer(event) {

      this.$emit("update:selectPlayer",event);
    }
  },
}
</script>

<style>

</style>