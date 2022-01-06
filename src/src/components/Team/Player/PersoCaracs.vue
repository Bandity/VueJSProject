<template>
  <div v-if="currentPlayer !== null" >
    <br/>
    <p>Name : {{ currentPlayer.name }} </p>
    <p>Level : {{ currentPlayer.level }} </p>
    <p>Life : {{ currentPlayer.life }} </p>
    <p>Armor : {{ currentPlayer.armor}} </p>
    <p>Vitality : {{ currentPlayer.vitality }} </p>
    <p>Strength : {{ currentPlayer.strength }} </p>
    <br/>
    <div>
      <label>Gold : </label>
      <input readonly="readonly" :value="currentPlayer.gold" /><br />
    </div>
    <br/>
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