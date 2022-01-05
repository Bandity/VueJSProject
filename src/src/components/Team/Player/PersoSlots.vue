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
    <div  v-if="currentPlayer !=null">
    <input readonly="readonly" :value="boughtItems" /><br />
    </div>
  </div>
</template>

<script>
export default {
  name: "PersoSlots",
  props: {
    currentPlayer: Object,
  },
  data: () => {
    return {
      boughtItems:0
    };
  },
};
</script>

<style>
</style>