<template>
  <div>
      <PersoSelector/>
      <Perso/>
  </div>
</template>

<script>
import PersoSelector from "./PersoSelector.vue";
import Perso from "./Perso.vue";
import {towns, team} from "../../model/model";
export default {
    name: "Team",
    props: {
        team: Array
    },
    components: {
        PersoSelector,
        Perso
    },
    data: ()=>{
        team,
        towns
    },
    computed:{
        
    }

}
</script>

<style>

</style>