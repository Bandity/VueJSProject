<template>
  <div v-if="currentPlayer !== null" >
    <p>Name : {{ currentPlayer.name }}</p>
    <p>Level : {{ currentPlayer.level }}</p>
    <p>Life : {{ currentPlayer.life }}</p>
  </div>
</template>

<script>
export default {
  name: "PersoCaracs",
  props: {
    currentPlayer: Object
  },
  data:() =>{
    return{
      
    };
  }
};
</script>

<style>
</style>