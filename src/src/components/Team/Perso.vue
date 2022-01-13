<template>
  <div>
    <PersoCaracs :currentPlayer="currentPlayer">
      <template v-slot:level="{ level }">
        <div style="display: flex">
          <p style="padding-left: 10px">
            Level : <span style="color: green">{{ level }}</span>
          </p>
        </div>
      </template>
      <template v-slot:gold="{ gold }">
        <div>
          <img src="../../assets/Player/coins.png" width="15px" height="15px" />
          <span style="padding-left: 10px; margin-bottom: 10px">{{
            gold
          }}</span>
        </div>
      </template>
    </PersoCaracs>
    <PersoSlots :currentPlayer="currentPlayer" />
    <PersoOps :currentPlayer="currentPlayer" :currentShop="currentShop" />
  </div>
</template>

<script>
import PersoCaracs from "./Player/PersoCaracs.vue";
import PersoOps from "./Player/PersoOps.vue";
import PersoSlots from "./Player/PersoSlots.vue";

export default {
  name: "Perso",
  components: {
    PersoCaracs,
    PersoOps,
    PersoSlots,
  },
  props: {
    currentPlayer: Object,
    currentShop: Object,
  },
  data: () => {
    return {};
  },
  computed: {},
  methods: {},
};
</script>

<style>
</style>