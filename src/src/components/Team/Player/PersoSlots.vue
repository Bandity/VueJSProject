<template>
  <div>
    <table border="1"  v-if="currentPlayer !== null">
      <tr v-for="(el, i) in currentPlayer.slots" :key="i">
        <td>{{ el.name }}</td>
        <td v-for="(item, index) in el.items" :key="index">
          [ {{ index }} ] - {{ item.name }}
        </td>
      </tr>
    </table>
    <br />
    <div  v-if="currentPlayer !=null" style="text-align: center; ">
    <input readonly="readonly" :value="currentPlayer.boughtItems" /><br />
    </div>
    <br/>
  </div>
</template>

<script>
export default {
  name: "PersoSlots",
  props: {
    currentPlayer: {
      boughtItems: Array
    }
  },
  data: () => {
    return {
    };
  },
};
</script>

<style>
</style>