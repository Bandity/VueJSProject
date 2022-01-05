<template>
  <div v-if="currentPlayer !== null" >
    <span>Name : {{ currentPlayer.name }} </span>
    <span>Level : {{ currentPlayer.level }} </span>
    <span>Life : {{ currentPlayer.life }} </span>
    <span>Armor : {{ currentPlayer.armor}} </span>
    <span>Vitality : {{ currentPlayer.vitality }} </span>
    <span>Strength : {{ currentPlayer.strength }} </span>
    <div>
      <input readonly="readonly" :value="currentPlayer.gold" /><br />
    </div>
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