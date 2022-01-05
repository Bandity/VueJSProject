<template>
  <div v-if="currentPlayer !== null" >
    <p>{{ currentPlayer.name }}</p>
    <p>{{ currentPlayer.level }}</p>
    <p>{{ currentPlayer.life }}</p>
  </div>
</template>

<script>
export default {
  name: "PersoCaracs",
  props: {
    currentPlayer: Object
  },
  data:() =>{

  }
};
</script>

<style>
</style>